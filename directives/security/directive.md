---
id: security
title: Distrust input, bound it, and destroy only what is meant
description: >
  Everything that reaches the code from outside is checked and bounded before it is used, an operation that removes
  data or files removes exactly what it means to, and nothing an operation creates is left behind when it ends.
applies-when: >
  writing or changing code that takes input from outside, builds queries, commands or paths, removes data or files,
  creates temporary files, streams, connections or locks, returns errors to the outside, adds a dependency, or
  changes configuration that needs a secret
precedence: >
  this directive wins over the project's convention — a hole is never kept for consistency, however common it is in
  the code around it
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- input from outside — a request, a message, a file, a header — is checked at the edge for type, format and allowed
  values, and becomes a value object before the domain sees it, see [value-objects](../value-objects/directive.md)
- everything from outside has a limit: the size of a body and of an uploaded file, the length of a text, the number
  of items in a list or a batch, the size of a page; a query driven from outside never returns an unbounded result
- a query, a command or a path built with input from outside passes that input as a parameter, never by
  concatenation — SQL, query languages, shell commands, file paths
- a path from outside is normalised and checked to stay inside the directory it is allowed in; a name from outside
  is never used as a file name as it is
- an operation that removes or overwrites data or files states exactly what it removes: by id, or by a condition that
  cannot widen to everything when a value is empty or missing; a recursive delete stays inside a directory the code
  itself owns
- the request object takes only the fields the caller may set; an id, an owner, a status or a price the caller must
  not choose is never bound from the request
- an error returned to the outside says what the caller can act on; a stack trace, a query, an internal path or an
  exception's own message stays in the log
- a new dependency comes from a known source, in a maintained version with no known vulnerability
- a password, a token, a key or any other secret reaches the code from outside the repository — an environment
  variable, or whatever secret store the project's infrastructure provides; never written into the code or into a
  committed file, a `docker-compose.yml`, an application configuration or a committed `.env` included
- a temporary file, a stream, a connection or a lock is released on every path out, failure included; what an
  operation created before it failed is removed or rolled back

Must not:

- deserialise data from outside into types the data itself chooses
- write secrets or personal data to a log — see [logging](../logging/directive.md)

## Examples

Before — the name from the request decides where the file is written, and a temporary file stays on failure:

```java
Path target = uploads.resolve(request.fileName());
Path temp = Files.createTempFile("upload", ".tmp");
copy(request.body(), temp);
scan(temp);
Files.move(temp, target);
```

After — the name is checked to stay in the uploads directory, the size is bounded, and the temporary file is removed
on every path:

```java
Path target = uploads.resolve(UploadName.from(request.fileName()).value()).normalize();
if (target.startsWith(uploads) && request.size() <= MAX_UPLOAD_BYTES) {
    Path temp = Files.createTempFile("upload", ".tmp");
    try {
        copy(request.body(), temp);
        scan(temp);
        Files.move(temp, target);
    } finally {
        Files.deleteIfExists(temp);
    }
}
```

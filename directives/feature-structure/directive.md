---
id: feature-structure
title: Organise by feature, not by layer
description: >
  Packages are organised by use case, each one self-contained. The four-part shape below is JVM-flavored terminology;
  the underlying idea — no shared technical layers, no shared entity classes across use cases — is language-agnostic.
applies-when: laying out packages, or deciding where a new class belongs
precedence: the project's existing package layout wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- packages are organised by use case, not by technical layer
- a use-case package is self-contained — its own entity representations, repository, events
- two use cases never share entity classes even when they map to the same table
- four-part shape — entrypoint (HTTP only) / use-case class / repository interface + db impl / domain entity

**When two use cases orchestrate the same aggregate** (`identify-aggregates` put both commands under one aggregate
because one persisted record must see every contending write — see its invariant-visibility check), this rule
still holds at the class level and does not contradict that decision: each use case still gets its own domain class
and its own repository port, tailored to only what that use case needs to decide. What must **not** duplicate is
the underlying persisted record — every use case's repository implementation reads and writes the same row/stream
for that aggregate id, through whatever transactional or locking boundary the storage provides. "Two use cases
never share entity classes" is a rule about the Java type, not about the data: giving each use case its own class
over one shared record is the correct shape, not an exception to it. Skipping the shared record and letting each
use case's class keep truly separate storage silently reintroduces the exact bug `identify-aggregates` exists to
catch — two write paths that cannot see each other's state — just one layer further down, in code instead of in
the event-storming model.

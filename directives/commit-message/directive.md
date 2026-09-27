---
id: commit-message
title: Write the commit message by the seven rules
description: >
  How a commit message is written — a short, capitalised, imperative subject; a blank line; a body wrapped at 72
  that explains what changed and why. Only the message: it never decides that a commit happens, which stays with
  the protocol's checkpoint and the developer.
applies-when: writing the message of a commit that the developer has already agreed to
precedence: >
  the project's own commit convention wins where it differs (a prefix scheme, a ticket format, a different length),
  read from its recent history or contributing guide
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`. Rules from Chris Beams, [How to Write a Git Commit
Message](https://cbea.ms/git-commit/).

## Directive

**This directive is not a permission to commit.** It applies only once a commit is already agreed — at a
protocol's blocking checkpoint, or on the developer's explicit request. It never makes a commit happen, never
suggests one, and never turns "the message is ready" into a reason to commit.

Must — the seven rules:

1. **Separate the subject from the body with a blank line.** Git treats everything up to the first blank line as
   the title.
2. **Limit the subject to 50 characters** — a rule of thumb; 72 is the hard limit.
3. **Capitalise the subject.**
4. **Do not end the subject with a period.**
5. **Use the imperative mood in the subject.** It must complete the sentence "If applied, this commit will
   _\<subject\>_": "Remove deprecated methods", not "Removed deprecated methods", "Removing…", or "More fixes".
6. **Wrap the body at 72 characters.**
7. **Use the body to explain what and why, not how.** Say why the change was made — how things worked before and
   what was wrong with that. The code already shows how; a change complex enough to need prose explaining how
   needs a source comment, not a commit message.

Also:

- A body is optional. When the change is simple enough that the subject says everything, one line is the whole
  message.
- If the subject is hard to write because the change does several things, the commit is too big — say so at the
  checkpoint rather than writing a vague subject; the split is the developer's call.
- References to an issue tracker go at the end of the body, one per line: `Resolves: #123`, `See also: #456`.
- A message with a body is passed whole — `git commit -F <file>` or `git commit -F -` from standard input — never
  squeezed into a single `-m`, which loses the line breaks.

## Examples

Breaks rules 3, 4 and 5, and says nothing about why:

    fixed the booking bug.

One line is enough for a simple change:

    Fix typo in the booking confirmation email

Subject, blank line, body wrapped at 72 that says why:

    Reject a reservation for a desk marked out of service

    A desk taken out of service still accepted reservations: the check
    looked only at existing reservations for the day, not at the desk's
    own status. Employees booked it and found it cordoned off.

    The service status is now part of the availability check, so the
    reservation is rejected with DeskOutOfService.

    Resolves: #214

---
id: defer-discovered-gaps
title: Park a coverage gap, don't derail
description: >
  Contrast with a genuinely new case for the behaviour being built right now, which gets a stub immediately. A gap in unrelated, pre-existing code spotted mid-task is different — record it and keep going; address it afterwards as its own separate run.
applies-when: any protocol, at any step — a coverage gap unrelated to the current task is spotted mid-work
precedence: none — this always applies, it does not compete with a project convention
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`. `applies-when: any` is a
universal scope: this directive is relevant everywhere, not tied to one situation.

## Directive

Must:

- never widen the current change to cover a newly spotted unrelated gap
- the deferred gap becomes a separate piece of work later
- tell the developer in one line when something is parked, and record it in the session's Parked list

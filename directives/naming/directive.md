---
id: naming
title: Domain-language names, verb-noun use cases
description: >
  Production code names come from the domain's ubiquitous language, not from technical roles.
applies-when: naming a class, method, or use case in production code
precedence: the project's existing naming convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- use cases are verb-noun (`CreateReservation`, `CloseVoting`)
- names follow the domain's ubiquitous language

Forbidden: `Impl` suffix, `util`, `manager`, `helper`, `handler`, `resolver`, vague `processor`.

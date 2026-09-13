---
id: abstraction-timing
title: Stay concrete until the second use case
description: >
  Generic abstraction is earned by a second real use case, not anticipated for a hypothetical future one.
applies-when: considering whether to generalise or extend a piece of code
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- no generic abstraction before a second real use case exists
- no extension points "for the future"
- apparent duplication is not merged until the shared meaning is real — weigh bounded contexts, SOLID, business meaning

---
id: determinism
title: No ambient time or randomness in business logic
description: >
  Business logic never reaches out to the ambient clock or a random source directly — both are injected, so behaviour is reproducible and testable.
applies-when: business logic needs the current time, a date, or a random value
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- never call `Instant.now()` / `LocalDate.now()` directly in business logic — inject a Clock and pass it into domain methods
- the same for random values and other non-deterministic sources

---
id: specifications
title: Explicit business rules as Specifications
description: >
  When a business rule is worth naming and composing, model it with the Specification pattern rather than an inline boolean expression.
applies-when: a business rule is reused, or complex enough that a name would clarify intent
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- specifications are named after the rule (`IsDeskAvailableInCycle`, `IsBookingCycleNotStarted`)
- compose with and / or / not rather than nesting conditionals

Applies when the rule is reused, or complex enough that a name clarifies intent — not to every boolean expression.

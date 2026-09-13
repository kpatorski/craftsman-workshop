---
id: test-naming
title: Name a test by the state it describes
description: >
  The name states the resulting behaviour or state, not a wish and not the implementation. It describes the scenario in the product owner's language — the PO knows the business rules, not whether method X was called.
applies-when: naming a test method
precedence: the project's existing naming convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- no wish prefixes (`shouldCreate...`, `testValidation`, `validNameTest`)
- no implementation terms in the name — no method names, no "calls X", no "passes Y"

Exception: a small utility class, or a case where method-level naming is genuinely clearer, may name the method instead
of the state.

## Examples

Good: `reservationIsCreatedWhenSlotIsAvailable`, `eventIsNotPublishedIfReservationFailed`, `emptyNameIsRejected`.

Bad: `shouldCreateReservation`, `testValidation`, `validNameTest`.

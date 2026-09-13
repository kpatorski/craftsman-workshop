---
id: acceptance-criteria-format
title: Acceptance criteria are the Given/When/Then rules, carried through
description: >
  Same philosophy as `test-naming` — state behaviour in the product owner's language, not implementation. A checklist, not prose. When the event(s) backing this spec have digested Given/When/Then rules attached, each criterion is that rule verbatim — not paraphrased or rewritten. Only write a fresh criterion when no digested rule covers the case.
applies-when: writing acceptance criteria for a spec
precedence: none — this always applies
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- each criterion is one observable, checkable statement, in Given/When/Then form where a rule exists for it
- criteria describe behaviour/outcome, not implementation steps
- a criterion sourced from a digested rule is copied as-is, so it reads the same in `business-rules.md` and in the spec

## Examples

    - [ ] Given desk is marked available for the requested day, when employee requests a reservation, then ReservationConfirmed
    - [ ] Given desk is already reserved for the requested day, when employee requests a reservation, then ReservationRejected

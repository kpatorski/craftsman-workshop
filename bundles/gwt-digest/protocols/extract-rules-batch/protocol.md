---
id: extract-rules-batch
title: Extract GWT rules for one section
description: >
  Extracts Given/When/Then rules for one section, stopping for confirmation before the next.
input: one section of the input from read-input
output: GWT rules for this section
checkpoint:
  type: ask
  blocking: true
  prompt: "Section <n> <title> — rules extracted: <list>. Complete? Right phrasing?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. For one section/story fragment, extract the business rules it implies as Given/When/Then statements.
2. One rule per distinct precondition/outcome pair.
3. Stop and confirm before moving to the next section.

## Examples

    ~~~rule
    id: reservation-confirmed-when-desk-available
    section: "Book a desk"
    given: Desk is marked available for the requested day
    when: Employee requests a reservation for that desk and day
    then: ReservationConfirmed
    ~~~

---
id: extract-rules-batch
title: Extract GWT rules for one section
description: >
  For one section/story fragment, extract the business rules it implies as Given/When/Then statements — one rule per distinct precondition/outcome pair. Stop and confirm before the next section.
input: one section of the input from read-input
output: GWT rules for this section
checkpoint:
  type: ask
  blocking: true
  prompt: "Section <n> <title> — rules extracted: <list>. Complete? Right phrasing?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [extract-rules](../extract-rules/protocol.md).

## Examples

    ~~~rule
    id: reservation-confirmed-when-desk-available
    section: "Book a desk"
    given: Desk is marked available for the requested day
    when: Employee requests a reservation for that desk and day
    then: ReservationConfirmed
    ~~~

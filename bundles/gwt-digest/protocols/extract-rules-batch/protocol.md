---
id: extract-rules-batch
title: Extract GWT rules for one section
description: >
  Extracts Given/When/Then rules for one section, confirms them, and appends them to business-rules.md
  immediately — never deferred to the end of the run. Found live: a 21-batch digest left every confirmed rule
  sitting only in the (gitignored, see EXECUTION.md) session file until finalize-digest's last step, so a
  developer watching the run had nothing real to read for the whole thing — "work done, invisible on disk".
input: one section of the input from read-input
output: GWT rules for this section, confirmed and already appended to business-rules.md
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
4. **Once confirmed, append this section's rules to business-rules.md in the same turn** — in the canonical block
   form below. Create the file (a one-line header naming the source) on the first batch; append on every batch
   after. Never wait for finalize-digest to write something a developer could already read right now.

## Examples

    ~~~rule
    id: reservation-confirmed-when-desk-available
    section: "Book a desk"
    given: Desk is marked available for the requested day
    when: Employee requests a reservation for that desk and day
    then: ReservationConfirmed
    ~~~

---
id: review-use-cases
title: Review the code use case by use case
description: >
  Walks the code of the change one use case at a time, in the order of `structure`, so every finding is read in the
  context of the use case it belongs to, never as a list of unrelated lines.
input: the review state with a confirmed `structure` and `rules`, and the triage explanations written
output: every use case in `structure` reviewed, its findings in the review state
steps: [review-use-case]
repeat-until: every use case in `structure` is `reviewed`
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

Repeat until the condition holds:

1. [review-use-case](../review-use-case/protocol.md) — the next use case not yet `reviewed`.

A file in several use cases is reviewed with the first use case that reaches it, and only once. The changed files no
use case reaches (the server lists them apart) are reviewed last, together, as a use case of their own, whose checks
are recorded under the use case `untied`.

## Examples

A PR with the use cases "Cancel a reservation" and "Release unpaid reservations" is reviewed in that order;
`ReservationRepository`, in both, is reviewed with "Cancel a reservation" and not again with the second.

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

1. Read the plan of the directive checks: run the plugin's `review_directives.py <review folder> --plan`, by its full
   path. It says which reviewers to start, each with its directives and files, which checks are `not-applicable` and
   why, and which `file` directives each use case records — worked out from the diff, `structure` and the `code-review`
   bundle's [directive-scope.md](../../directive-scope.md), never chosen by the agent.
2. Start the plan's `file` reviewers — `use-case` null — once for the whole change, before any use case:
   `EXECUTION.md`'s "Independent directive review", steps 2–4 and 6, each reviewer with its own files' part of the diff
   and its own directives, all started in the same turn, each with `model: "sonnet"`, and the developer's `context` from
   the review state when there is one. A `VIOLATION` or `CONVENTION` that holds becomes a finding as
   [review-use-case](../review-use-case/protocol.md)'s steps 3 and 6 say, stored at once.
3. Repeat until the condition holds: [review-use-case](../review-use-case/protocol.md) — the next use case not yet
   `reviewed`.

A file in several use cases is reviewed with the first use case that reaches it, and only once. The changed files no
use case reaches (the server lists them apart) are reviewed last, together, as a use case of their own, whose checks
are recorded under the use case `untied`.

## Examples

A PR with the use cases "Cancel a reservation" and "Release unpaid reservations" is reviewed in that order;
`ReservationRepository`, in both, is reviewed with "Cancel a reservation" and not again with the second. `naming`, a
`file` directive, is checked once, by one reviewer over every production file of the change, before either use case;
`module-dependencies`, a `flow` one, is checked in each use case.

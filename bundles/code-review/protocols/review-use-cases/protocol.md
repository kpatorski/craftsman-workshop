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
   path. It says which reviewers to start, each with its directives, its files and, for a `flow` reviewer, the use cases
   it takes; which checks are `not-applicable` and why; and which `file` directives each use case records — worked out
   from the diff, `structure` and the `code-review` bundle's [directive-scope.md](../../directive-scope.md), never
   chosen by the agent.
2. Start every reviewer of the plan before the first use case, all in the same turn, each with `model: "sonnet"`:
   `EXECUTION.md`'s "Independent directive review", steps 2 and 3, each reviewer on the part of the diff of its own
   files, with its own directives, the worktree's path to look up whatever else its code relies on, and the developer's
   `context` from the review state when there is one. A `flow` reviewer is told its use cases, each with its files and
   its steps from `structure`, and reports every finding under the use case it belongs to. Keep every report: each use
   case takes its part in [review-use-case](../review-use-case/protocol.md)'s step 3.
3. Repeat until the condition holds: [review-use-case](../review-use-case/protocol.md) — the next use case not yet
   `reviewed`.

A file in several use cases is reviewed with the first use case that reaches it, and only once. The changed files no
use case reaches (the server lists them apart) are reviewed last, together, as a use case of their own, whose checks
are recorded under the use case `untied`.

## Examples

A PR with the use cases "Cancel a reservation" and "Release unpaid reservations" is reviewed in that order;
`ReservationRepository`, in both, is reviewed with "Cancel a reservation" and not again with the second. `naming`, a
`file` directive, is checked once, by one reviewer over every production file of the change; `module-dependencies`,
a `flow` one, by one reviewer that takes both use cases, each as its own flow, because together they change fewer
than 1500 lines. All of them start before the first use case.

---
id: map-change-structure
title: Map the structure of the change
description: >
  Finds the shape of the change before any of its code is judged — the use cases it adds or changes, the bounded
  contexts it touches, how they talk to each other — and groups every changed file into a PR map the reviewer can
  find their way around by.
input: the review state with a confirmed `scope` and `requirements` (`read-pr-scope`)
output: the review state's `structure` and `map`, confirmed by the developer
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Shown on the review page, with the graph of use cases and contexts, and summed up here: "The change has <n> use
    cases: <name — entry point, one per line>. It touches <contexts>. Boundaries: <one sentence>. Not covered by any
    use case: <requirements, or none>. Not asked for by any requirement: <use cases, or none>. Is this the shape?"
    Options: the shape is right; correct it (a note).
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

This step reads to find the shape, never to judge: names, signatures and calls, not the quality of the code. Nothing
it notices becomes a finding here; what looks wrong goes into `boundaries` as a note for
[review-use-cases](../review-use-cases/protocol.md).

1. List the changed files: `git diff --name-status <base>...<head>`, read in the review's worktree.
2. Find the entry points the change adds or changes — the places where something outside the code calls in: an HTTP
   endpoint, a message listener, a scheduled job, a command-line command, a public method of a module's API. Every
   entry point is one use case; its `entry` is the file and line where it starts.
3. From each entry point, follow the calls down only as far as needed to know which changed files belong to that use
   case. A file reached from several use cases belongs to none of them alone — it goes to a shared group in step 7.
4. Name every use case in the language of the requirements, verb and noun ("Cancel a reservation"), never after the
   class that implements it.
5. Find the bounded contexts the change touches — the modules or top-level packages the project already has, named
   the way the project names them. Note every use case that crosses from one into another.
6. Write `boundaries`: how the parts talk to each other (a direct call, an event, HTTP, a shared table), and every
   place where a dependency points in a direction that looks wrong — a domain class reaching into infrastructure, one
   context reading another's tables. Record every pair of contexts that talk in this change as a `link`, with how they
   talk and, for a wrong-looking direction, why — the page draws the graph from these.
7. Build the PR map: every changed file in exactly one group. One group per use case, with the tests that test it;
   then groups for what serves several use cases or none — a shared model, configuration, database migrations, the
   build. One or two sentences per group on what it does in this PR, written for someone who has not read the code.
8. Compare with the requirements: a requirement no use case covers, and a use case no requirement asks for. These are
   questions for the checkpoint, not findings.
9. Store all of it with `review_state.py`, then stop at the checkpoint. A correction is written into `structure` or
   `map` before the review goes on.

A large change — many entry points, or many files per use case — is read in parts, one part per use case, as
delegated read-only preparation (`EXECUTION.md`); the groups, the names and the checkpoint stay in the run itself.

## Examples

A PR adds `POST /reservations/{id}/cancel` and a nightly job that releases unpaid reservations. Two use cases:
"Cancel a reservation" (entry: the controller's method) and "Release unpaid reservations" (entry: the job). A
`ReservationRepository` method both call goes to the group "Reservation storage", not to either use case.

The ticket asks for an e-mail to the customer after a cancellation; no changed file sends one. The checkpoint names
the requirement as covered by no use case — the e-mail may be in another PR, or missing.

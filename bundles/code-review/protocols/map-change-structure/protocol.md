---
id: map-change-structure
title: Map the structure of the change
description: >
  Finds the shape of the change before any of its code is judged — the use cases it adds or changes, the files each
  one reaches, and how each one runs from its entry point down — so the reviewer can read the change use case by use
  case.
input: the review state with a confirmed `scope` and `requirements` (`read-pr-scope`)
output: the review state's `structure`, confirmed by the developer
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Shown on the review page, with the use cases as cards, and summed up here: "The change has <n> use cases: <name —
    entry point, one per line>. Files no use case reaches: <paths, or none>. Calls across a boundary: <one per line, or
    none>. Not covered by any use case: <requirements, or none>. Not asked for by any requirement: <use cases, or
    none>. Is this the shape?" Options: the shape is right; correct it (a note).
---

## Schema

Introduces no new fields — see `core.md`. What `structure` holds is described in the plugin's `REVIEW.md`.

## Protocol

This step reads to find the shape, never to judge: names, signatures and calls, not the quality of the code. Nothing
it notices becomes a finding here; a call that looks wrong is recorded on its step as `crosses`, a note for
[review-use-cases](../review-use-cases/protocol.md).

1. List the changed files: `git -C <worktree> diff --name-status <base>...<head>`. Git runs in the worktree through
   `-C`, never after a `cd`: the review's headless session refuses a `cd` followed by `git`.
2. Find the entry points the change adds or changes — the places where something outside the code calls in: an HTTP
   endpoint, a message listener, a scheduled job, a command-line command, a public method of a module's API, and in a
   user interface a user's action or a route. Every entry point is one use case; its `entry` is the file and line
   where it starts.
3. Give each use case its changed files, in this order:
    1. **calls** — from the entry point, follow the calls down through the changed code; every changed file they
       reach belongs to the use case;
    2. **types** — every changed file declaring a type the use case's steps use: a parameter, a return value, a field,
       an object they create, an exception they throw;
    3. **package** — a changed file still in no use case belongs to the use case whose files share its package, when
       exactly one does. When two or more do, it stays in none.

   A file reached from several use cases belongs to each of them. A changed file in no use case is listed apart by
   the server, so none is lost; each is a question for the checkpoint.
4. Name every use case in the language of the requirements, verb and noun ("Cancel a reservation"), never after the
   class that implements it. Write, per [engineer-prose](../../directives/engineer-prose/directive.md), `says` — one
   sentence on what it does, for someone who has not read the code — and `before` and `after`: how the system
   behaves in this use case without the change and with it, one to three sentences each, in the same terms.
5. Write its `flow`:
    - `steps` — the calls from the entry point down, one per unit the use case passes through, each with its file
      and line and whether the change added, modified, deleted it or left it unchanged, and in `from` the path and
      line of the call that reaches it — every step but the entry point has one. A step whose call crosses a
      boundary the project keeps — a domain class reaching into infrastructure, one module into another's internals —
      names that boundary in `crosses`.
    - `branches` — the ways the use case can end (refused, done, failed), each with whether a test covers it.
6. Compare with the requirements: a requirement no use case covers, and a use case no requirement asks for. These are
   questions for the checkpoint, not findings.
7. Store `structure` with `review_state.py`, then stop at the checkpoint. A correction is written into `structure`
   before the review goes on.

A large change — many entry points, or many files per use case — is read in parts, one part per use case, as
delegated read-only preparation (`EXECUTION.md`); the names, the flows and the checkpoint stay in the run itself.

## Examples

A PR adds `POST /reservations/{id}/cancel` and a nightly job that releases unpaid reservations. Two use cases:
"Cancel a reservation" (entry: the controller's method) and "Release unpaid reservations" (entry: the job).
`ReservationRepository`, which both call, is in the files of both. `CancellationRequest`, the record the controller
passes to the service, is called by no one but is a parameter of a step, so it is in "Cancel a reservation" too. A
changed `CancellationPolicy` that no step names, in the package of "Cancel a reservation" only, joins that use case. A
changed `docker-compose.yml` no use case reaches is in neither; the checkpoint asks why it is in the PR.

"Refund in full" calls `billing.internal.RefundGateway` instead of billing's public `Billing`: that step's `crosses`
says "billing.internal", and the page draws the call in red.

The ticket asks for an e-mail to the customer after a cancellation; no changed file sends one. The checkpoint names
the requirement as covered by no use case — the e-mail may be in another PR, or missing.

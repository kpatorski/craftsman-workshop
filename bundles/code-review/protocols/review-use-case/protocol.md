---
id: review-use-case
title: Review one use case, from its entry point down
description: >
  Reads one use case's code from its entry point down — module, class, method, parameters — checks it against the
  enabled directives, and has independent reviewers check the same code, so the findings do not depend on one reader's
  blind spots. Every finding is written as a proposed PR comment and shown on the page at once.
input: one use case from the review state's `structure`, with its files
output: the use case `reviewed`, its findings in the review state
checkpoint:
  type: notify
  prompt: >
    "Use case <k> of <n>, <name>: <m> findings — <count per kind>. Directives: <c> checked — <x> with findings,
    <y> not applicable, <z> not checked and why. Next: <name of the next use case, or the end of the walk>."
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

The review reads and writes findings; it never edits the code and never posts anything — sending is the developer's,
from the page. Code is read in the review's worktree; git runs there as `git -C <worktree> …`, never after a `cd`.

1. Mark the use case `reviewing`. Collect the criteria: the directives of the plan's `flow` reviewers that took this use
   case (`review_directives.py <review folder> --plan`, read in [review-use-cases](../review-use-cases/protocol.md));
   the `file` directives are checked over the whole change, not per use case. The developer switches the directives on
   the review page, and the plan leaves none out because it seems not to fit: the reviewers say which do not apply.
   [review-posture](../../directives/review-posture/directive.md) and
   [review-comment](../../directives/review-comment/directive.md) are not among them; they govern how every finding
   below is kinded and written.
2. Walk the use case from its `entry` down, one level at a time, each level before the next:
    - **module** — which modules the use case passes through, what each depends on, and whether those dependencies
      cross a boundary in `structure` the wrong way;
    - **class** — each class the use case reaches: what it is responsible for, its name, its visibility, what it
      depends on;
    - **method** — each method on the path: what its signature promises read alone, with the body collapsed; how it
      decides to do its work; its size;
    - **parameters** — each parameter and return type: whether it says what the value is, and whether it belongs to
      the layer it crosses.

   At every level, check what the change adds or changes against the criteria, and for every unit it adds, go down
   [simplest-solution](../../../../directives/simplest-solution/directive.md)'s ladder: a simpler form that holds is
   a `simplify` finding. Look at the unchanged code of the
   units the change works inside too, and at what the use case reaches outside the change — that is where `scout` and
   `out-of-scope` findings come from.
3. Take this use case's part of the independent check, started for the whole change in
   [review-use-cases](../review-use-cases/protocol.md): what the `flow` reviewers reported under this use case, and what
   the `file` reviewers reported in its files that no earlier use case took. Verify it as `EXECUTION.md`'s "Independent
   directive review" step 4 says; a reviewer that failed or left a directive out is run again once, as its step 6 says,
   for this use case's part. Step 4 never fixes anything here: a `VIOLATION` that holds is a `violation` finding; a
   `CONVENTION` that holds is a `new-convention` finding when the changed code is a new unit, otherwise a `scout`
   finding — see `review-posture`. Step 5 does not run, because nothing is fixed.
4. Merge the walk's findings with the reviewers': the same problem at the same place is one finding. The same problem
   at several places of this use case is one finding with several locations, the first being the clearest.
5. Bring in what earlier steps left as questions: a requirement no test states, a rule that contradicts one, a use
   case with no test change, a step whose call `crosses` a boundary. Each becomes a finding only when an enabled
   directive covers it; otherwise it stays the question it already is.
6. Write every finding per `review-comment`, in the review's comment language: `category`, `title`, `description`,
   `comment`, `locations` (with the `head` commit), `directive`, `kind`, `severity`, and `when` for `out-of-scope`.
   `severity` is how much it costs to merge the code as it is:
    - `must-fix` — it breaks a requirement, loses or exposes data, or opens a security hole;
    - `should-fix` — it works, but makes the code harder to change or to trust, and is cheap to fix now;
    - `nit` — a small matter of naming or form the reviewer would not hold the PR for.

   Store each with `review_state.py` as `proposed` as soon as it is written, so the page fills while the walk goes on.
7. Record what every directive found in this use case, all in one `review_state.py <review folder> record-check`
   with a list of `{"use-case": "<id>", "directive": "<id>", "result": ..., "note": ...}`:
    - for each criterion of step 1:
        - `findings` — a finding of this use case names the directive;
        - `clean` — its reviewer found nothing, or nothing that held;
        - `not-applicable` — its reviewer said so; its reason goes in `note`;
        - `failed` — its group failed twice (step 6 of the independent review); say so at the checkpoint;
    - for each `file` directive the plan's `file-checks` gives this use case: `findings` when a finding naming it has
      a location in this use case's files, `failed` when its reviewer failed twice, else `clean`;
    - every check the plan's `not-applicable` gives this use case, as it is, with its `note`.

   A directive with no record is a gap, never reported as clean.
8. Mark the use case `reviewed`, then notify.

## Examples

"Cancel a reservation", entry `ReservationController.cancel`:

- module: the controller's module imports `billing.internal.RefundCalculator` — a dependency across contexts into
  another module's internals; `violation` if a directive on module dependencies is enabled.
- class: the new `CancellationService` is public, its neighbours are public too, and only its package uses it →
  `new-convention`, pointing at a public neighbour.
- method: `cancel(...)` starts with three `if (...) return;` exits before its work → `violation` under the directive
  on method exits, its comment proposing one named condition.
- parameters: `cancel(String reservationId, String userId)` → a finding under `value-objects`, with both parameters
  as one finding with two locations.
- every directive the plan gives goes to the reviewers: `module-dependencies` reports the import of
  `billing.internal.RefundCalculator`, recorded as `findings`; `security`, with no input from outside in the use case,
  is recorded as `not-applicable`, "no input from outside". `no-explanatory-comments`, a `file` directive, found the
  comments above `cancel(...)` before the use cases, so it is recorded here as `findings` too; `test-naming`, with no
  test file in the use case, is recorded as the plan says: `not-applicable`, "no test files in this use case".

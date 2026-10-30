---
id: review-posture
title: An existing convention changes a finding's kind, never whether it exists
description: >
  The reviewer respects the project's conventions and other people's style, and does not push one right way. But a
  bad pattern being common is never a reason to repeat it: new code may set a better convention, touched code is
  left cleaner, and a problem outside the PR's scope is still written down.
applies-when: deciding whether something seen in a review becomes a finding, and of which kind
precedence: >
  within a review, overrides the default that the project's convention wins — an existing convention decides a
  finding's kind, never removes it
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- a finding comes from an enabled directive; a personal preference no directive states is not a finding — the review
  does not push one right way
- every rule a directive states is checked, even where the project breaks it everywhere; "we do it like this
  everywhere" is never a reason to drop a finding
- each finding gets exactly one kind:
  - `violation` — the changed code breaks a rule the project otherwise keeps;
  - `new-convention` — the changed code breaks a rule the same way existing code does, and the changed code is a new
    unit (module, set of classes, class, method): new code is where a better convention starts;
  - `scout` — the change works inside an existing unit that breaks a rule, whether or not this PR introduced the
    breakage: the proposal is to leave that unit cleaner than the PR found it;
  - `out-of-scope` — a problem the review saw in code the PR does not touch: it is still written down, marked `now`
    (worth doing in this PR) or `later` (a follow-up), so the history shows it was seen
- a change that leaves the code worse than before is a `violation`, never a `scout`
- a `new-convention` finding points at one existing place that does the same, so the author sees the pattern is
  known, not overlooked

Must not:

- silence a finding because the author followed an existing pattern
- turn a `scout` or `out-of-scope` finding into a demand: it is a proposal, and its comment says so — see
  [review-comment](../review-comment/directive.md)

## Examples

- A new `PaymentService` class is public, like every other class in the module, while only its own package uses it
  → `new-convention`: the new class can be package-private even though its neighbours are not.
- The PR adds two lines to an existing 300-line `OrderManager` → `scout`: propose extracting the part the PR touched,
  not rewriting the class.
- The PR adds a third early `return;` to a method that had two → `violation`: the method is harder to read than
  before.
- While following a use case, the review sees `DeskRepository` exposing a mutable list in a module the PR does not
  change → `out-of-scope`, `later`.

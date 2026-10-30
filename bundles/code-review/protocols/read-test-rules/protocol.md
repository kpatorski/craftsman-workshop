---
id: read-test-rules
title: Read the business rules from the tests
description: >
  Reads the tests the change adds or changes as statements of business rules, and sets each rule against the
  requirements — before any production code is read, so the reviewer knows what the change promises before checking
  how it keeps that promise.
input: the review state with a confirmed `requirements` and `structure` (`map-change-structure`)
output: the review state's `rules`, each tied to its test and to the requirement it covers, confirmed by the developer
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Shown on the review page and summed up here: "The tests state <n> rules: <rule — test, one per line>. In conflict
    with a requirement: <list, or none>. Requirements no test states: <list, or none>. Rules no requirement asks for:
    <list, or none>. Use cases with no test change: <list, or none>. Are these the rules?" Options: the rules are
    right; correct them (a note).
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

This step reads tests only. A rule that lives only in production code is not guessed from it here — it shows up when
[review-use-cases](../review-use-cases/protocol.md) reads the code.

1. For each use case in `structure`, take the tests in its group of the PR map that the change adds or changes. Note
   every use case whose production code changes with no test change at all.
2. Read each test as a statement of a rule: its name, what it sets up, what it does, what it expects. Write the rule
   as one sentence in the language of the requirements — "A reservation cannot be cancelled less than an hour before
   it starts" — never as a description of the test.
3. One rule per distinct rule, not per test: a parametrised test, or several tests of one rule with different data,
   give one rule with every test listed. A test that checks only technical behaviour (mapping, serialisation, wiring)
   states no business rule; it is counted, not listed.
4. Tie each rule to the requirement it covers, or record that none does.
5. Compare the other way: every requirement no rule states, and every rule that contradicts a requirement — the test
   expects one outcome, the ticket asks for another. A contradiction is the first thing the checkpoint names.
6. Store the rules with `review_state.py`, then stop at the checkpoint. A correction is written into `rules` before the
   review goes on. What is missing or contradictory here is a question, not a finding; it becomes a finding only in
   `review-use-cases`, and only when an enabled directive covers it.

A change with many tests is read in parts, one part per use case, as delegated read-only preparation (`EXECUTION.md`);
the comparison with the requirements and the checkpoint stay in the run itself.

## Examples

`CancelReservationTest` has `refuses cancellation less than an hour before the start` and `allows cancellation an hour
or more before the start`, both stating one rule — "A reservation cannot be cancelled less than an hour before it
starts" — which covers the second acceptance criterion of `BOOK-42`.

`BOOK-42` also asks that a cancelled reservation is refunded in full; no test expects a refund. The checkpoint names it
as a requirement no test states — the refund may be untested, or not built.

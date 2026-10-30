---
id: pr-review
title: Review a pull request in a HUMAN <-> AI loop
description: >
  Entry point for reviewing one pull request, or the difference between two branches of the checked-out repository.
  Understanding is confirmed with the developer before any code is judged; the findings go to the review page, where
  the developer edits, picks and sends them. Nothing is ever posted to GitHub without the developer sending it.
input: >
  a GitHub pull request URL, or `<target>:<source>` naming two branches of the repository checked out in the current
  directory, plus optionally `session=<path>`
output: >
  the review state under `.claude/reviews/<review-id>/` (see the plugin's `REVIEW.md`), shown on the review page, with
  every use case of the change reviewed; the session stays open, serving the page, until the developer closes it
entry-point: true
steps: [open-review, read-pr-scope, map-change-structure, read-test-rules, triage-explanations, review-use-cases,
  deduplicate-findings, serve-page]
done-when: the developer closes the review
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [open-review](../../bundles/code-review/protocols/open-review/protocol.md) — read the PR or the two branches,
   create the review state, open the review page.
2. [read-pr-scope](../../bundles/code-review/protocols/read-pr-scope/protocol.md) — what the PR is for, from its
   description and the requirements it links.
3. [map-change-structure](../../bundles/code-review/protocols/map-change-structure/protocol.md) — the use cases,
   bounded contexts and boundaries the change touches, and the PR map.
4. [read-test-rules](../../bundles/code-review/protocols/read-test-rules/protocol.md) — the business rules the tests
   state, against the requirements.
5. [triage-explanations](../../bundles/code-review/protocols/triage-explanations/protocol.md) — short explanations
   of the places that are hard to follow without context.
6. [review-use-cases](../../bundles/code-review/protocols/review-use-cases/protocol.md) — the code, use case by use
   case, from the entry point down.
7. [deduplicate-findings](../../bundles/code-review/protocols/deduplicate-findings/protocol.md) — one finding per
   problem, with every place it occurs.
8. [serve-page](../../bundles/code-review/protocols/serve-page/protocol.md) — answer what the developer asks from the
   page until they close the review.

Session file handling, directive loading, and resuming are the execution mechanics described in the `craftsman` skill
itself, not repeated per protocol — see [implement](../implement/protocol.md) for the same note.

## Examples

`/craftsman:pr-review https://github.com/org/booking/pull/123` reviews PR 123 of the repository checked out in the
current directory. `/craftsman:pr-review main:feature/cancel-reservation` reviews what `feature/cancel-reservation`
adds on top of `main`; if a PR exists for that branch, its comments can be sent there.

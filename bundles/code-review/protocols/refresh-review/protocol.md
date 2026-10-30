---
id: refresh-review
title: Bring the review up to date with the PR
description: >
  Reads the PR or the branches again after the author pushed or replied: moves the review to the new head, reviews
  only the use cases the new commits touch, marks findings that may be resolved, and shows the author's replies — never
  deleting a finding and never changing what the developer wrote.
input: a review in `serve-page`, and a `refresh` request from the page
output: the review state at the new `head`, its findings re-checked, the replies to sent comments recorded
checkpoint:
  type: notify
  prompt: >
    "Refreshed to <head, short sha> (<k> new commits). Re-reviewed: <use cases, or none>. New findings: <n>. Maybe
    resolved: <findings, or none>. New replies: <count per finding, or none>. Description or tickets changed: <what, or
    no>."
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Fetch what is reviewed, as [open-review](../open-review/protocol.md) does, without touching the developer's
   working tree. For a PR, read its description, and the replies to every comment the review has sent, with `gh`.
2. Record every new reply under its finding's `sent` entry with `review_state.py`. A reply is shown on the page; it
   is never answered from here.
3. When the head has not moved, stop here: record `refreshed`, then notify.
4. Move the review's worktree to the new head (`git -C <worktree> checkout --detach <head>`), store the diff of
   `base...head`, and record the new `base`, `head` and `refreshed`.
5. When the description or the tickets changed, compare them with `scope` and `requirements` and name what differs in
   the notification. They are not rewritten without the developer: a correction comes as a message.
6. Find what the new commits changed: `git diff <old head>..<head> --name-only`. Every use case with a changed file
   goes back to `pending`. A changed file in no group of the PR map is placed in a group, or in a new use case, the
   way [map-change-structure](../map-change-structure/protocol.md) places it.
7. Re-check every finding that is not `deleted`, `merged` or `sent`, at the new head:
    - its lines moved — update its locations;
    - the problem is gone — set `maybe-resolved`; only the developer decides it is resolved;
    - the problem is still there — leave it.

   A `sent` finding whose problem is gone is named in the notification; it is not changed.
8. Run [review-use-cases](../review-use-cases/protocol.md) for the use cases back in `pending`, then
   [deduplicate-findings](../deduplicate-findings/protocol.md), then notify. Findings already in the review are not
   written again: a problem already found keeps its finding.

## Examples

The author pushes two commits fixing `f2` and `f5` and adding a test. `f2` and `f5` become `maybe-resolved`; "Cancel a
reservation", whose test changed, is reviewed again and gives no new findings; the notification names the two
findings and the use case.

The author replies to the sent `f3`: "The id is a String because the API contract says so." The reply is shown under
`f3` on the page; the developer decides whether to answer it on GitHub.

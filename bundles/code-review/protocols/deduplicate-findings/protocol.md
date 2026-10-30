---
id: deduplicate-findings
title: Make one finding of each problem
description: >
  Joins the findings of different use cases that are one problem into one finding with every place it occurs, so the
  author reads the problem once and every other place points back to it.
input: the review state with every use case `reviewed`
output: one finding per problem, every other copy marked `merged` with the finding it went into
checkpoint:
  type: notify
  prompt: >
    "Joined <x> findings into <y>. The review has <n> findings — <count per kind>, <count per category>. Every use case
    is reviewed; the findings are on the page to edit, delete or mark to send."
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

`review-use-case` already joins the copies of a problem within one use case; this step joins them across use cases.

1. Find the candidates: findings from the same directive, of the same kind, in different use cases.
2. Two findings are one problem when one comment fits every place they point at, with only the place changing — the
   same rule broken the same way, with the same proposed solution. The same directive alone is not enough: two
   different value objects missing are two problems, not one. A `violation` and a `scout` finding stay two findings
   even when the rule is the same, because they ask for different things.
3. Choose the finding the others go into: the one the developer has edited, marked to send, or sent, if any — the
   developer's text wins; otherwise the one whose first location is earliest in the walk. Its first location stays
   where the comment goes; the others' locations are added after its own, in the order of the walk.
4. Never join two findings the developer has both edited, marked to send, or sent: a text the developer wrote is not
   replaced by another the developer wrote. Leave them as they are; a question about it goes into the notification.
5. Store it with `review_state.py`: the chosen finding gets the added locations; every other copy gets `merged` and
   `merged-into`, never removed — the page shows it folded under the finding it went into.

## Examples

"Cancel a reservation" has a finding under `value-objects` for `String reservationId` in `CancellationService.cancel`;
"Release unpaid reservations" has the same finding for `String reservationId` in `ReleaseJob.release`. One finding,
two locations: the comment goes on `CancellationService.cancel`, and `ReleaseJob.release` gets a short "same as" link
when the review is sent.

`naming` finds `ReservationManager` in one use case and `PaymentHelper` in another: two findings — the names break
the same rule, but each needs its own new name.

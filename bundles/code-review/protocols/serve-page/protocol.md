---
id: serve-page
title: Answer the review page until the review is closed
description: >
  Keeps the review's session working for the developer after the walk is done: every request sent from the review
  page — an explanation, a question, a refresh, a message typed into the console — is handled as it arrives, until
  the developer closes the review.
input: the review state with every use case `reviewed` and the findings deduplicated
output: every request from the page handled; the review `closed`
steps: [refresh-review]
repeat-until: the developer closes the review
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

The dashboard server passes each line of the review's inbox into this session as a message, one at a time, after the
previous one is handled — see the plugin's `REVIEW.md`, "`inbox.jsonl`". Between messages the session waits; it
never polls.

For each message, by its `type`, then record its `id` in `handled` with `review_state.py`:

- `explain` — add a `requested` explanation about the group, file or finding it names, and write it the way
  [triage-explanations](../triage-explanations/protocol.md) writes one: short, engineer to engineer, never a made-up
  reason.
- `ask` — answer the question in a new `requested` explanation about the same thing, so the answer stays on the page
  next to what it is about.
- `refresh` — run [refresh-review](../refresh-review/protocol.md).
- `message` — answer in the console, as in a CLI conversation. When it asks for a change to a finding, change only
  the fields the developer has not edited; for an edited field, show the proposed text in the console and leave it to
  the developer to take it on the page. When it asks for a new finding, add it: from a directive, written per
  [review-comment](../../directives/review-comment/directive.md); or, when the developer states the problem
  themselves, with no directive and the developer's point as its substance.
- `answer` — an answer to a checkpoint that is no longer open: say so in the console, and ask whether it changes
  anything already done.
- `close` — set `closed` in the review state and end the run. The state and the worktree stay; the review can be
  opened again with the same PR or branches.

Sending to GitHub is never handled here: the page sends through the server, and the session sees the result as
`sent` in the review state.

## Examples

The developer clicks Explain on the group "Reservation storage" → a `requested` explanation of how the repository
locks a reservation row while it is cancelled, shown under the group.

In the console: "Make f4 shorter." `f4`'s comment is not edited → it is rewritten in place. Then: "Make f7 shorter."
`f7`'s comment was edited by the developer → the shorter text is shown in the console, and `f7` stays as it is.

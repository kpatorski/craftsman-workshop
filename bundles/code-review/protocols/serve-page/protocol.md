---
id: serve-page
title: Answer the review page until the review is closed
description: >
  Keeps the review's session working for the developer after the walk is done: every request sent from the review
  page — a question about a finding, a file's lines, a use case or the whole review, a refresh, a directive to
  check, a new context — is handled as it arrives, until the developer closes the review.
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

- `ask` — read the thread it names and reply in the same thread (`reply`), per
  [engineer-prose](../../directives/engineer-prose/directive.md), never a made-up reason. The thread's `about` and
  `quote` say what the question is about; answer about that. When it asks for a change to a finding, change only the
  fields the developer has not edited; for an edited field, reply with the proposed text and leave it to the developer
  to take it on the page. When it asks for a new finding, add it: from a directive, written per
  [review-comment](../../directives/review-comment/directive.md); or, when the developer states the problem themselves,
  with no directive and the developer's point as its substance. Say in the reply what was changed or added.
- `refresh` — run [refresh-review](../refresh-review/protocol.md).
- `check` — the developer switched on the directive it names after use cases were reviewed. Read the plan again
  (`review_directives.py <review folder> --plan`) and start that directive's reviewers alone, as the plan packs them: a
  `file` directive over its files, a `flow` one on the use cases already `reviewed`, and `untied` once reviewed — as
  [review-use-case](../review-use-case/protocol.md) steps 3, 4, 6 and 7 do, all started in the same turn. Add what
  holds as findings, record the results with one `record-check`, the plan's `not-applicable` checks for it included,
  and say in the console how many findings it made in which use cases.
- `context` — the developer added a note to the review's `context` or took one back. Read the notes, work by them
  from the next step on, and say in the console in one sentence what that changes in the review; use cases already
  reviewed are not reviewed again unless the developer asks.
- `answer` — an answer to a checkpoint that is no longer open: say so in a thread about the whole review, and ask
  whether it changes anything already done.
- `close` — set `closed` in the review state and end the run. The state and the worktree stay; the review can be
  opened again with the same PR or branches.

Sending to GitHub is never handled here: the page sends through the server, and the session sees the result as
`sent` in the review state.

## Examples

The developer selects lines 22–23 of `CancellationService.java` and asks "Is this the refusal from AC1?" → a reply in
that thread: yes, the only owner check, and what the caller gets back.

In the thread of `f4`: "Make it shorter." `f4`'s comment is not edited → it is rewritten in place, and the reply says
so. In the thread of `f7`, the same: `f7`'s comment was edited by the developer → the reply carries the shorter text,
and `f7` stays as it is.

---
id: refresh-review
title: Bring the review up to date with the PR
description: >
  Reads the PR or the branches again after the author pushed or replied: moves the review to the new head, reviews
  only the use cases the new commits touch, marks findings that may be resolved, and reads what was said on the PR
  since — never deleting a finding, never changing what the developer wrote, never answering on GitHub.
input: a review in `serve-page`, and a `refresh` request from the page
output: the review state at the new `head`, its findings re-checked against the code and what was said on the PR
checkpoint:
  type: notify
  prompt: >
    "Refreshed to <head, short sha> (<k> new commits). Re-reviewed: <use cases, or none>. New findings: <n>. Maybe
    resolved: <findings, or none>. On GitHub since the last refresh: <answers per sent finding, other new comments, or
    nothing; or why it could not be read>. Description or tickets changed: <what, or no>."
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Fetch what is reviewed, as [open-review](../open-review/protocol.md) does, without touching the developer's
   working tree. For a PR, read its description with `gh`.
2. For a PR, read its conversation again: run the plugin's `github_conversation.py <review folder>`, by its full path,
   then read `github.json` in the review folder — the plugin's `REVIEW.md`, "`github.json`", says what it holds. What
   is new is what is dated after `refreshed`. When the script says GitHub did not answer, name the reason in the
   notification and go on without the conversation.
3. Read what is new:
    - an answer in the thread of a sent finding — the thread whose `root` is the comment the finding's `sent` link
      points at — is named under that finding in the notification;
    - an answer that explains why the code is as it is, or says the finding is wrong, is weighed: when it changes the
      finding, say so in a note on it (`open-thread` about the finding), quoting the answer;
    - any other new comment is counted in the notification.

   Nothing is answered on GitHub from here; that is the developer's, from the page.
4. When the head has not moved, stop here: record `refreshed`, then notify.
5. Move the review's worktree to the new head (`git -C <worktree> checkout --detach <head>`), store the diff of
   `base...head`, and record the new `base`, `head` and `refreshed`.
6. When the description or the tickets changed, compare them with `scope` and `requirements` and name what differs in
   the notification. They are not rewritten without the developer: a correction comes as a message.
7. Find what the new commits changed: `git -C <worktree> diff <old head>..<head> --name-only`. Every use case with a
   changed file goes back to `pending`. A newly changed file is added to every use case whose calls reach it, or to a
   new use case, the way [map-change-structure](../map-change-structure/protocol.md) places it; a file none reaches
   stays out of every use case, and the server lists it apart.
8. Re-check every finding that is not `deleted`, `merged` or `sent`, at the new head:
    - its lines moved — update its locations;
    - the problem is gone — set `maybe-resolved`; only the developer decides it is resolved;
    - the problem is still there — leave it.

   A `sent` finding whose problem is gone is named in the notification; it is not changed.
9. Run [review-use-cases](../review-use-cases/protocol.md) for the use cases back in `pending`, then
   [deduplicate-findings](../deduplicate-findings/protocol.md). Findings already in the review are not written again:
   a problem already found keeps its finding.
10. A finding not yet sent whose problem someone already raised on GitHub, at the same place, gets a note
    (`open-thread` about the finding) with the link to that comment, so the developer can drop it. Then notify.

## Examples

The author pushes two commits fixing `f2` and `f5` and adding a test. `f2` and `f5` become `maybe-resolved`; "Cancel a
reservation", whose test changed, is reviewed again and gives no new findings; the notification names the two
findings and the use case.

The author answers the sent `f3` on GitHub: "The id is a String because the API contract says so." The notification
names the answer under `f3`, and a note on `f3` quotes it and says that it changes the finding only if the contract
is outside the PR. The developer reads the thread under Comments, and answers it there or not.

Another reviewer comments on `CancellationService.java:41`: "This catches every exception." The proposed `f9` says
the same of the same line, so `f9` gets a note with the link to that comment.

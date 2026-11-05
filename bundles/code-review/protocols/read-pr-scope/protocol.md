---
id: read-pr-scope
title: Read what the PR is for
description: >
  States what the change is for — from the PR's description and the Jira tickets it links — before any code is read,
  so everything after it is judged against what was asked, not against what happens to be in the diff.
input: the review state from `open-review`
output: the review state's `scope`, `requirements` and `tickets`, confirmed by the developer
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Shown on the review page and summed up here: "PR <number> — <scope in one sentence>. Requirements: <n> from
    <tickets>, or why there are none. Differences between the description and the tickets: <list, or none>. Is
    this the scope?" Options: the scope is right; correct it (a note); and, when Jira could not be read, paste the
    requirements, or continue without them.
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read what the author wrote: the PR's title and description. Without a PR, read the commit messages of
   `base..head` and the source branch's name instead, and say on the page that there is no description. Read the
   developer's `context` from the review state, when there is one: it says what the description does not.
2. Find the Jira tickets: keys (`ABC-123`) and Jira links in the title, the description and the branch name.
3. Read each ticket with whatever Jira access this environment has — its summary, description and acceptance
   criteria. No access, or a ticket that cannot be read: record why in `requirements`, never guess what the ticket
   says, and offer the developer to paste it at the checkpoint.
4. Write the `scope` in three short parts, per [engineer-prose](../../directives/engineer-prose/directive.md):
   **Before** — how the system behaves today in the part the PR touches; **After** — how it behaves once the PR is
   merged, and why; **Left out** — what the description says the PR does not do. Write the `requirements`: what the
   tickets ask for, one item per requirement, each with its ticket key.
5. Note every place where the description, the tickets and the developer's `context` disagree — a requirement the
   description does not mention, something the description adds that no ticket asks for. These are questions for the
   checkpoint, not findings yet.
6. Store all of it with `review_state.py`, then stop at the checkpoint. A correction is written into `scope` or
   `requirements` before the review goes on; pasted requirements are recorded as given by the developer.

## Examples

The description says "Adds cancelling a reservation"; the ticket `BOOK-42` also asks that a cancellation is refused
less than an hour before the reservation starts. The checkpoint names that rule as missing from the description — the
review later checks whether the code has it.

A PR with no ticket in its description, title or branch: `requirements` says so, and the checkpoint asks whether to
continue without requirements or take them from the developer.

---
id: open-review
title: Open a review
description: >
  Reads the pull request or the two branches, gives the review its own worktree at the reviewed commit, creates the
  review state, and opens the review page. The developer's working tree and branches are never touched, so several
  reviews and the developer's own work can run side by side in one repository.
input: >
  a GitHub pull request URL, or `<target>:<source>` naming two branches; the repository checked out in the current
  directory
output: >
  `.claude/reviews/<review-id>/` with `review.json` (source, `base`, `head`), the diff, and a `worktree/` at `head`;
  the comment language settled; the review page open
checkpoint:
  type: ask
  blocking: true
  when: the PR's description is written in a language other than English
  prompt: >
    "The description of PR <number> is in <language>. Comments are written in English by default — write them in
    English, or in <language>?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read the source:
    - a PR URL — `gh pr view <url>` for its number, title, description, base and head branches and commits. The PR's
      repository must be the one checked out here (`gh repo view`); if it is not, stop and say which repository to
      run the review from.
    - `<target>:<source>` — both branches must exist locally or on `origin`. Look up an open PR for the source branch
      with `gh pr list --head <source>`; if there is one, the review is attached to it exactly as if its URL had been
      given; if there is none, the review runs without one, and the page says sending is unavailable.
2. Name the review: `pr-<number>`, or `<target>..<source>` with every `/` replaced by `-`. If
   `.claude/reviews/<review-id>/` already exists, this is a review already in progress: resume it, never overwrite
   it — starting over is the developer's decision, asked, never assumed.
3. Fetch what is reviewed — `git fetch origin <base-branch>` and, for a PR, `git fetch origin pull/<number>/head` —
   without checking anything out in the developer's working tree.
4. Add `.claude/reviews/` to `.git/info/exclude` if it is not there yet — the review's files stay out of `git status`
   without changing the repository's own `.gitignore`.
5. Create the worktree: `git worktree add --detach .claude/reviews/<review-id>/worktree <head>`. Every file the review
   reads, it reads here — the developer's checkout may be on another branch, or mid-change.
6. Create the review state with `review_state.py init` — source, `base` (the merge base of target and head), `head`,
   and the diff `base...head`. The PR in `source` carries its `title`, `base-branch` and `head-branch`; the page shows
   them in its header.
7. Settle the comment language: English when the description is in English or there is no PR; otherwise stop here
   and ask (the checkpoint above), and record the answer in the review state.
8. Open the review page: `dashboard_server.py on --project <repository>`, and print the review's URL on its own line.

## Examples

`/craftsman:pr-review https://github.com/org/booking/pull/123` in a clone of `org/booking` → review `pr-123`, worktree
at the PR's head commit, the developer's own branch left as it was. Run again later for the same URL → the same
review, resumed.

`/craftsman:pr-review main:feature/cancel-reservation` with an open PR #130 for that branch → review
`main..feature-cancel-reservation`, attached to PR #130. Without a PR → the same review, sending disabled.

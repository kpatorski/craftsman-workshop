---
id: open-review
title: Open a review
description: >
  Reads the pull request or the two branches, gives the review its own worktree at the reviewed commit, creates the
  review state. The developer's working tree and branches are never touched, so several reviews and the developer's
  own work can run side by side in one repository.
input: >
  a GitHub pull request URL, or `<target>:<source>` naming two branches; the review's folder (`--review`) and the
  repository's checkout (`--checkout`), both given by the dashboard server, which runs this session in the checkout
output: >
  the review's folder with `review.json` (source, checkout, `base`, `head`), the diff, and a `worktree/` at `head`;
  the comment language settled
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
      repository must be the one checked out here (`gh repo view`); if it is not, stop and say which checkout the
      review needs.
    - `<target>:<source>` — both branches must exist locally or on `origin`. Look up an open PR for the source branch
      with `gh pr list --head <source>`; if there is one, the review is attached to it exactly as if its URL had been
      given; if there is none, the review runs without one, and the page says sending is unavailable.
2. The review's folder is the one after `--review`. If it already holds `review.json`, this is a review already in
   progress: resume it, never overwrite it — starting over is the developer's decision, asked, never assumed.
3. Fetch what is reviewed — `git fetch origin <base-branch>` and, for a PR, `git fetch origin pull/<number>/head` —
   without checking anything out in the developer's working tree.
4. Create the worktree: `git worktree add --detach <review folder>/worktree <head>`. Every file the review reads, it
   reads here — the developer's checkout may be on another branch, or mid-change.
5. Write the diff `base...head` into the review's folder — `git diff --output=<review folder>/init.diff
   <base>...<head>`, where `base` is the merge base of target and head — and create the review state with it:

   ```
   review_state.py <review folder> init '{"source": {...}, "checkout": "<path after --checkout>",
     "base": "<sha>", "head": "<sha>", "diff": "<review folder>/init.diff"}'
   ```

   `init` moves the diff to `diff/<head>.diff`. `source` is `{"kind": "pull-request", "url", "repository", "number",
   "title", "base-branch", "head-branch"}`, or `{"kind": "branches", "target", "source", "pull-request"}` with the
   same PR object or null — see `REVIEW.md`; the page shows the title and the branches in its header.
6. Settle the comment language: English when the description is in English or there is no PR; otherwise stop here
   and ask (the checkpoint above), and record the answer in the review state.

## Examples

`https://github.com/org/booking/pull/123` with a checkout of `org/booking` → review `org-booking-pr-123`, worktree at
the PR's head commit, the developer's own branch left as it was. Started again later for the same URL → the same
review, resumed.

`main:feature/cancel-reservation` in the checkout `~/code/booking`, with an open PR #130 for that branch → review
`booking-main..feature-cancel-reservation`, attached to PR #130. Without a PR → the same review, sending disabled.

---
id: review-comment
title: A review comment sounds like a teammate talking to a teammate
description: >
  A proposed PR comment reads the way a colleague would say it at the author's desk: short, plain, about the code and
  never about the person. It says what the problem is and what to do; why it matters only when that is not obvious.
  The author should be able to act on it without a follow-up question.
applies-when: writing or editing the proposed PR comment of a review finding
precedence: >
  a review-comment convention the team has agreed on (required labels, a template) wins on form; the rules on tone
  never yield
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- as long as the point needs and no longer: a reminder or a small thing is one or two sentences; a problem that needs
  explaining gets a short paragraph or two. The developer's own draft sets the size — a one-line thought stays short.
- what is wrong and what to do; the consequence only when the author would not see it themselves — "this branch is
  gone after the merge" needs no paragraph on what a missing branch does
- spoken, plain English, the way it would be said aloud: "we", "let's", "I'd" are fine; a real question is fine when
  the reviewer does not know the answer ("Do we still need the retry here?")
- in English, unless the developer chose another language for this review — a PR whose description is in another
  language is a question to the developer before the first comment is written, never a guess
- one problem per comment — two problems are two findings
- a code snippet only when the fix is not clear from a sentence, and then only the lines that change
- an `out-of-scope` finding says so first and whether it is for this PR or a follow-up — so the history shows the
  topic was seen, not skipped
- a `new-convention` finding says the existing code does it the other way and why new code need not
- every location after the first gets one line pointing at the first comment, not a copy of it

Must not:

- repeat what the comment sits on: the file, the line number, the names the diff shows right above it
- formal or report language: "it should be noted", "in order to", "ensure that", "the aforementioned", headings, bold
  labels like "Problem:" / "Fix:"
- a person as the cause: "you forgot", "your code" — the code is the subject, or "we"
- judgement words: wrong, bad, ugly, lazy, sloppy, terrible, obviously, simply, just
- rhetorical or accusing questions ("why would you…?", "did you even…?")
- sarcasm, irony, or exclamation marks

## Examples

Good — a reminder stays a reminder:

> Reminder: this `qa` stage for the feature branch has to go before we merge to `main` — the branch won't exist
> after that.

Bad — the same reminder as a report:

> The new `cd.stages` entry at `ci/config.json:11` deploys `feature/x` to `qa`. This branch is removed before the PR
> is merged to `main`, so the entry would point at a branch that no longer exists.
>
> Remove that entry in the same change that merges to `main`. Only the `main` → `qa` stage should remain: (…)

Good — a problem that needs a reason and a fix:

> Three early `return;`s before the actual work make it hard to see when this cancels anything, and the next rule
> change will have to find all three. I'd fold them into one named condition:
>
> ```java
> if (reservation.isCancellableBy(employee)) {
>     reservation.cancel();
> }
> ```

Bad:

> Why did you write it like this? This is really messy, just use one if.

Out of scope:

> Not for this PR, but worth a follow-up: `DeskRepository` is public and only `booking` uses it. Package-private
> would keep other modules off how desks are stored.

Further locations:

> Same as [this comment](https://github.com/org/repo/pull/123#discussion_r1).

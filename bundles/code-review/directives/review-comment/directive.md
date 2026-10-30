---
id: review-comment
title: A review comment names the problem, its consequence, and a fix
description: >
  A proposed PR comment is short, about the code and never about the person, and always in three parts: what the
  problem is, why it matters, and what to do instead. The author should be able to act on it without a follow-up
  question.
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

- three parts, in this order:
  1. **the problem** — what the code does here, pointing at the concrete line, name or call;
  2. **why it matters** — the consequence: for the next reader, for the next change, or in production;
  3. **the proposal** — what to do instead, concretely; a short code snippet when it says more than a sentence would.
- in English, unless the developer chose another language for this review — a PR whose description is in another
  language is a question to the developer before the first comment is written, never a guess
- one problem per comment — two problems are two findings
- short: a few sentences per part, readable without scrolling; cut every sentence the author does not need to act
- the subject is the code, never the person: "this method", "here", "the new class" — not "you", "your code"
- a neutral or friendly tone, the way one engineer explains something to another
- an `out-of-scope` finding says so in its first sentence and says whether it is worth doing in this PR or in a
  follow-up — so the history shows the topic was seen, not skipped
- a `new-convention` finding acknowledges the existing pattern elsewhere and says why new code need not repeat it
- every location after the first gets one line pointing at the first comment, not a copy of it

Must not:

- judgement words: wrong, bad, ugly, lazy, sloppy, terrible, obviously, simply, just
- rhetorical or accusing questions ("why would you…?", "did you even…?")
- sarcasm, irony, or exclamation marks
- restating what the diff already shows without saying what is wrong with it

## Examples

Good:

> `ReservationService.cancel` returns early in three places (`if (!x) return;`), so the reader has to collect the
> conditions to learn when it actually cancels anything.
>
> The next change to the rules will have to find all three, and a missed one cancels when it should not.
>
> Combining them into one named condition keeps the rule in one place:
>
> ```java
> if (reservation.isCancellableBy(employee)) {
>     reservation.cancel();
> }
> ```

Bad:

> Why did you write it like this? This is really messy, just use one if.

Out of scope:

> Outside this PR's scope, worth a follow-up: `DeskRepository` is public, while only `booking` uses it. Making it
> package-private would keep other modules from depending on how desks are stored.

Further locations:

> Same as [this comment](https://github.com/org/repo/pull/123#discussion_r1).

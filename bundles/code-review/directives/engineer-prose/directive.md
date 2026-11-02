---
id: engineer-prose
title: Review texts read like one engineer briefing another
description: >
  Every text a pull-request review writes for the developer — what the PR is for, the use cases, notes, answers in
  threads, a finding's description — states facts from the code, short and in plain words, with no filler.
applies-when: >
  writing a text of a pull-request review the developer reads: the PR's scope, a use case's `says`, `before` and
  `after`, a note, a reply in a thread, a finding's description
precedence: >
  `review-comment` governs the form of a proposed PR comment; this directive adds to it and never loosens it. It
  applies to pull-request reviews only, not to the texts of other craftsman commands.
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- name things the way the code does: the class, the method, the endpoint, the table, the configuration key — not "the
  service", "the logic", "the flow"
- numbers over adjectives: "3 callers", "1 h before the start", "+40 lines" — not "several", "shortly", "a lot"
- one fact per sentence, the one that matters most first
- say what changes and what it costs; what the diff already shows is left out unless it is the point
- something unknown is said in one sentence: what is unknown, and where it would be found
- `before` and `after` describe the same behaviour in the same terms — how the system behaves in this place without
  the change, and how it behaves once it is merged — so the difference stands out

Must not:

- introductions and wrap-ups: "This PR introduces…", "In summary", "Overall", "Let me explain"
- filler and hedging: basically, essentially, simply, it is worth noting, it seems that, various, robust, seamless,
  leverage
- restating the question at the start of an answer
- praise, marketing tone, or emphasis by adjectives

## Examples

Good — a use case's `before` and `after`:

> Before: a reservation cannot be cancelled; it ends when its time passes.
>
> After: `POST /reservations/cancel` marks it `CANCELLED` up to 1 h before the start, calls `Billing.refund` for the
> full amount, and e-mails the owner.

Bad — the same with filler and no facts:

> This PR introduces a robust new cancellation flow that seamlessly integrates with billing and notifications,
> essentially allowing users to cancel their reservations in various scenarios.

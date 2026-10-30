---
id: triage-explanations
title: Explain the places that are hard to follow
description: >
  Writes, unasked, a few short explanations — engineer to engineer — of the places in the change a reviewer is likely
  to stop at: why it is done this way and how it works in this context. Only the few that matter most; every other
  place is explained when the developer asks for it on the page.
input: the review state with a confirmed `structure`, `map` and `rules` (`read-test-rules`)
output: at most five `triage` explanations in the review state, each about a group of the PR map or a file
checkpoint:
  type: notify
  prompt: >
    "Explained <n> places: <what each is about, one per line>. <m> other places could use an explanation — ask for one
    on the page with Explain."
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

An explanation explains; it never judges. What looks wrong while writing one is left for
[review-use-cases](../review-use-cases/protocol.md) — it is not a finding here, and not hinted at in the explanation.

1. Find the candidates — places in the change a reviewer cannot follow from the code in front of them alone:
    - a pattern new to this project — look for it elsewhere in the repository before calling it new;
    - concurrency: locks, threads, retries, idempotency, ordering of messages;
    - transaction boundaries, and what happens when one part fails after another succeeded;
    - configuration or framework behaviour that changes what the code does without being visible in it;
    - security: who may call it, what comes from outside, secrets, cryptography;
    - an algorithm that is not obvious from its code;
    - a migration that changes existing data.
2. Rank them by how much a reviewer loses without the explanation, and take at most five. Count the rest; they are
   not written.
3. Write each one short — a few sentences, at most a short list — for an engineer who knows the language and the
   framework but not this code:
    - what it does in this change;
    - why it is done this way — from the code, the commit messages, the PR's description, the tickets. When none of
      them says why, write that the reason is not in the change and is a question for the author; never make one up;
    - how it works in this context — the part that is not visible in the lines themselves;
    - what to look at when reviewing it.
4. Store each explanation with `review_state.py` as soon as it is written, `pending` while it is written and `ready`
   when done, so the page shows them one by one. Then notify.

Writing the explanations may be done side by side, one per explanation, as delegated read-only preparation
(`EXECUTION.md`); choosing which places to explain stays in the run itself.

## Examples

A use case retries sending a payment with `@Retryable`, and the payment provider's client sends an idempotency key
built from the reservation id. Explanation: retries are safe because the provider ignores a second request with the
same key; the key is built in `PaymentRequestFactory`, and a reviewer should check that every retried call goes
through it.

A new outbox table and a job that publishes from it, where the project publishes events directly everywhere else. The
explanation says what the outbox guarantees (an event is published only when the transaction that wrote it commits)
and that the PR does not say why this use case needs it and others do not — a question for the author.

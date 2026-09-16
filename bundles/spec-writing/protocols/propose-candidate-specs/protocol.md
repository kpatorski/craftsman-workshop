---
id: propose-candidate-specs
title: Turn use cases into a candidate spec list
description: >
  Turns confirmed use cases into a candidate spec list.
input: event-model.md's `## Use cases` and `## Bounded contexts` sections, written incrementally during event-storming
output: an ordered list of candidate spec titles, each tagged with its source use case(s) and a task shape
uses: [one-task-granularity, classify-task-shape]
checkpoint:
  type: ask
  blocking: true
  prompt: "Candidate specs: <list, proposed merges marked>. Add, drop, merge, or split?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read `event-model.md`'s confirmed use cases — and any new-module bootstrap needs surfaced by its bounded
   contexts — and propose one candidate spec title per task. This is a read, not a re-derivation from the
   conversation: every use case and context it needs was already written there, section by section, during
   `event-storming-loop`.
2. Small, tightly-coupled use cases on the same aggregate may be proposed as one merged candidate — never merged
   silently, always flagged as a proposal.

---
id: collect-events
title: Collect every domain event, Big Picture style
description: >
  Collects every domain event from the input, Big Picture style, and starts event-model.md — the visible,
  incrementally-built record every later step in this loop appends to (see MANAGEMENT.md-style rationale in
  attach-rules-batch: a long model-building run with nothing written to disk until the very end leaves confirmed
  work invisible for its whole duration).
input: the raw input and any digested rules from ingest
output: an ordered list of domain events, confirmed and already written to event-model.md
checkpoint:
  type: ask
  blocking: true
  prompt: "Events found, in order: <list>. Complete? Right names, right order?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read the input end to end — the raw text and, where present, the digested Given/When/Then rules together.
2. List every domain event: a significant, past-tense, domain-language change in the system.
3. When rules are present, treat their `then` clauses as strong candidates — but this is still a judgement call, not a
   mechanical copy: merge duplicates, and don't promote a trivial rule outcome to event status.
4. Work in rough chronological order, breadth-first — capture everything before judging it.
5. **Once confirmed, create `event-model.md`** in the project root (a one-line header naming the source, then a
   `## Events` section listing them in order) — the first write of the run; every later step adds its own entries
   to this same file as they are confirmed, slice by slice, never waiting for `draw-bounded-contexts` to close it.

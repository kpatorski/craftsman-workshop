---
id: collect-events
title: Collect every domain event, Big Picture style
description: >
  Collects every domain event from the input, Big Picture style.
input: the raw input and any digested rules from ingest
output: an ordered list of domain events
checkpoint:
  type: ask
  blocking: true
  prompt: "Events found, in order: <list>. Complete? Right names, right order?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Read the input end to end — the raw text and, where present, the digested Given/When/Then rules together.
2. List every domain event: a significant, past-tense, domain-language change in the system.
3. When rules are present, treat their `then` clauses as strong candidates — but this is still a judgement call, not a mechanical copy: merge duplicates, and don't promote a trivial rule outcome to event status.
4. Work in rough chronological order, breadth-first — capture everything before judging it.

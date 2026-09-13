---
id: propose-candidate-specs
title: Turn use cases into a candidate spec list
description: >
  From the confirmed use cases (and any new-module bootstrap needs surfaced by bounded contexts), propose one candidate spec title per task. Small, tightly-coupled use cases on the same aggregate may be proposed as one merged candidate — never merged silently.
input: the confirmed use cases and bounded contexts from event-storming
output: an ordered list of candidate spec titles, each tagged with its source use case(s) and a task shape
uses: [one-task-granularity, classify-task-shape]
checkpoint:
  type: ask
  blocking: true
  prompt: "Candidate specs: <list, proposed merges marked>. Add, drop, merge, or split?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [requirements-analysis](../requirements-analysis/protocol.md).

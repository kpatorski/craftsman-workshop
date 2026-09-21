---
id: pick-first-aggregate
title: Pick the first aggregate to implement
description: >
  Picks the first aggregate to implement, from the domain-design output.
input: the aggregates produced by domain-design
output: the chosen first aggregate and its first use case
checkpoint:
  type: ask
  blocking: true
  when: the task does not already name which use case to build first
  prompt: "Domain design gives aggregates <list>. Start with <aggregate> and its <case>?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. From the domain-design output, choose the aggregate to build first. When the task already names the use case —
   as `slice-loop` does, having settled the order with the developer — that use case is the first; there is nothing
   to choose, and nothing to ask again.
2. Hand its first case to [scenario-new-use-case](../../../../protocols/scenario-new-use-case/protocol.md).

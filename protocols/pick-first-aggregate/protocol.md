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
  prompt: "Domain design gives aggregates <list>. Start with <aggregate> and its <case>?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. From the domain-design output, choose the aggregate to build first.
2. Hand its first case to [scenario-new-use-case](../scenario-new-use-case/protocol.md).

Used by: [bootstrap-module](../bootstrap-module/protocol.md).

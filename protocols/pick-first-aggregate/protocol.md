---
id: pick-first-aggregate
title: Pick the first aggregate to implement
description: >
  From the domain-design output, choose the aggregate to build first and hand its first case to scenario-new-use-case.
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

Used by: [bootstrap-module](../bootstrap-module/protocol.md).

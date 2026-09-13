---
id: draw-bounded-contexts
title: Draw bounded contexts and how they communicate
description: >
  Group aggregates into bounded contexts and settle how each pair of contexts talks — events, or a synchronous call.
input: the aggregates identified by identify-aggregates
output: bounded contexts, each with its aggregates and communication style (events / sync)
checkpoint:
  type: ask
  blocking: true
  prompt: "Bounded contexts: <list + communication style>. Confirm before moving to specs?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [event-storming](../event-storming/protocol.md).

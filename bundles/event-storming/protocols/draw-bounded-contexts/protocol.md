---
id: draw-bounded-contexts
title: Draw bounded contexts and how they communicate
description: >
  Draws bounded contexts and settles how they communicate.
input: the aggregates identified by identify-aggregates
output: bounded contexts, each with its aggregates and communication style (events / sync)
checkpoint:
  type: ask
  blocking: true
  prompt: "Bounded contexts: <list + communication style>. Confirm before moving to specs?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Group aggregates into bounded contexts.
2. Settle how each pair of contexts talks — events, or a synchronous call.

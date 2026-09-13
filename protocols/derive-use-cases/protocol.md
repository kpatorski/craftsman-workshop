---
id: derive-use-cases
title: Derive use cases from command + aggregate + event
description: >
  Derives candidate use cases from command + aggregate + event triples.
input: commands, aggregates and events from the preceding event-storming steps
output: a list of candidate use cases
checkpoint:
  type: notify
  prompt: "Use cases derived: <list>."
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. For each command/aggregate/event triple that represents one coherent operation, name it as a candidate use case.
2. This is the seed for a spec — default 1:1, mergeable at review in propose-candidate-specs.

Used by: [event-storming](../event-storming/protocol.md).

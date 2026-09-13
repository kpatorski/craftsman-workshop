---
id: derive-use-cases
title: Derive use cases from command + aggregate + event
description: >
  Each command/aggregate/event triple that represents one coherent operation becomes a candidate use case — the seed for a spec (default 1:1, mergeable at review).
input: commands, aggregates and events from the preceding event-storming steps
output: a list of candidate use cases
checkpoint:
  type: notify
  prompt: "Use cases derived: <list>."
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [event-storming](../event-storming/protocol.md).

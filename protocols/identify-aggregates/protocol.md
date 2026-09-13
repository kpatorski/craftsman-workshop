---
id: identify-aggregates
title: Group events under the aggregate that owns them
description: >
  Group events (with their rules) under the aggregate responsible for them, and draw the aggregate boundary.
input: events and their attached rules
output: aggregates, each with its owned events and rules
checkpoint:
  type: ask
  blocking: true
  prompt: "Aggregates: <name -> events>. Boundaries right?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [event-storming](../event-storming/protocol.md).

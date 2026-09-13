---
id: identify-aggregates
title: Group events under the aggregate that owns them
description: >
  Groups events under the aggregate that owns them.
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

1. Group events, with their rules, under the aggregate responsible for them.
2. Draw the aggregate boundary.

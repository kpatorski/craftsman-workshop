---
id: derive-commands
title: Derive the command that triggers each event
description: >
  Derives the command that triggers each event.
input: aggregates with their owned events
output: one command per event, attached to its aggregate
checkpoint:
  type: notify
  prompt: "Commands derived: <command -> event>; …"
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. For each event, name the command whose handling produces it — the intent that, when carried out, results in that
   event.

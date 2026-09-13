---
id: attach-rules-batch
title: Attach rules for a batch of events
description: >
  Attaches the rules for one batch of events, stopping for confirmation before the next.
input: a batch of events from collect-events
output: precondition phrases (or attached rule ids) for the events in this batch
checkpoint:
  type: ask
  blocking: true
  prompt: "Rules attached — <event>: <phrases>; … Continue to the next batch, or adjust?"
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. For a small batch of events, attach the digested rule(s) that produced each.
2. If no digested rules exist, write the precondition phrases directly instead.
3. Stop and confirm before moving to the next batch.

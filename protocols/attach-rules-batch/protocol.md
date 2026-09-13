---
id: attach-rules-batch
title: Attach rules for a batch of events
description: >
  For a small batch of events, attach the digested rule(s) that produced each (or write the precondition phrases directly, if no digested rules exist). Stop and confirm before the next batch.
input: a batch of events from collect-events
output: precondition phrases (or attached rule ids) for the events in this batch
checkpoint:
  type: ask
  blocking: true
  prompt: "Rules attached — <event>: <phrases>; … Continue to the next batch, or adjust?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [attach-event-rules](../attach-event-rules/protocol.md).

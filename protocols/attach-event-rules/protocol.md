---
id: attach-event-rules
title: Attach the rules that must hold for each event
description: >
  Each event gets the precondition phrases that must be true for it to fire. When digested Given/When/Then rules are available, this is mostly confirmation — attach the rule(s) whose `then` produced this event, using their `given` as the preconditions — rather than inventing from scratch. Without digested rules, write short precondition phrases directly: sticky notes above the event card, not a full sentence (e.g. "Resource is available", "User has role ADMIN").
input: the events collected by collect-events, plus digested rules if present
output: every event has its rules attached and confirmed
steps: [attach-rules-batch]
repeat-until: every event has its rules attached and confirmed
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). Replaces the old `loop` kind —
see `repeat-until`.

## Protocol

Repeat until the condition holds, processed in small batches, each stopping for confirmation:

1. [attach-rules-batch](../attach-rules-batch/protocol.md)

Used by: [event-storming](../event-storming/protocol.md).

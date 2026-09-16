---
id: event-storming-loop
title: Event storming from a requirements input
description: >
  Big Picture event storming run against the input document. Breadth-first: collect everything before judging any of it.
  Produces the building blocks a use case needs.
input: the input read by ingest, plus restate-understanding's confirmed summary
output: >
  events, their rules, aggregates, commands, views, use cases and bounded contexts, all confirmed and already in
  event-model.md — each step writes its own section as it is confirmed, not just the last one
steps: [collect-events, attach-event-rules, identify-aggregates, derive-commands, derive-views, derive-use-cases,
  draw-bounded-contexts]
done-when: events, their rules, aggregates, commands, views, use cases and bounded contexts are all confirmed
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [collect-events](../collect-events/protocol.md)
2. [attach-event-rules](../attach-event-rules/protocol.md)
3. [identify-aggregates](../identify-aggregates/protocol.md)
4. [derive-commands](../derive-commands/protocol.md)
5. [derive-views](../derive-views/protocol.md)
6. [derive-use-cases](../derive-use-cases/protocol.md)
7. [draw-bounded-contexts](../draw-bounded-contexts/protocol.md)

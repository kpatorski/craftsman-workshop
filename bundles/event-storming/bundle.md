---
id: event-storming
title: Event storming from a requirements input
description: >
  The Big Picture event-storming method, sliced: collect every domain event first, for the whole input, then take
  one use case at a time — attach its rules, group its events under an aggregate, derive its commands, read models
  and use case. Ends with bounded contexts drawn between the pieces that don't belong in the same one.
---

## Schema

No fields of its own — see `core.md`.

## Bundle

Input is a requirements text, plus optionally a `business-rules.md` (the [gwt-digest](../gwt-digest/bundle.md)
bundle's output, or written by hand) with Given/When/Then rules already extracted — authoritative when present,
not a hard dependency. Output is a full picture: events, each with its aggregate, commands, views, use cases, and
the bounded contexts between them.

Big Picture first, then one slice at a time: `collect-events` names every event for the whole input — cheap, and
it gives every later step sight of the siblings an aggregate's invariants depend on. Everything after that is
`model-slice`, run for one use case at a time, so a developer can judge the direction on the first complete example
before the rest are modelled the same way. The cost is that an aggregate drawn from one slice can need revising when
a later one arrives; every step that finds this names it as a revision rather than re-cutting a boundary silently.

## Protocols

**Enabled**

| No | Id                                                                   | Title                                             |
|----|----------------------------------------------------------------------|---------------------------------------------------|
| 1  | [model-slice](protocols/model-slice/protocol.md)                     | Model one use-case slice, from rules to use case  |
| 2  | [collect-events](protocols/collect-events/protocol.md)               | Collect every domain event, Big Picture style     |
| 3  | [attach-event-rules](protocols/attach-event-rules/protocol.md)       | Attach the rules that must hold for each event    |
| 4  | [attach-rules-batch](protocols/attach-rules-batch/protocol.md)       | Attach rules for a batch of events                |
| 5  | [identify-aggregates](protocols/identify-aggregates/protocol.md)     | Group events under the aggregate that owns them   |
| 6  | [derive-commands](protocols/derive-commands/protocol.md)             | Derive the command that triggers each event       |
| 7  | [derive-views](protocols/derive-views/protocol.md)                   | Derive the read models the use cases will need    |
| 8  | [derive-use-cases](protocols/derive-use-cases/protocol.md)           | Derive use cases from command + aggregate + event |
| 9  | [draw-bounded-contexts](protocols/draw-bounded-contexts/protocol.md) | Draw bounded contexts and how they communicate    |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

None. Every rule this bundle applies while modelling belongs to `spec-writing` or stays fundament.

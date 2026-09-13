---
id: event-storming
title: Event storming from a requirements input
description: >
  The Big Picture event-storming method: collect every domain event first, then attach the rules, group events
  under their aggregate, and derive the commands, read models and use cases each one implies. Ends with bounded
  contexts drawn between the pieces that don't belong in the same one.
---

## Schema

No fields of its own — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Bundle

Input is a requirements text, plus optionally a `business-rules.md` (the [gwt-digest](../gwt-digest/bundle.md)
bundle's output, or written by hand) with Given/When/Then rules already extracted — authoritative when present,
not a hard dependency. Output is a full picture: events, each with its aggregate, commands, views, use cases, and
the bounded contexts between them.

Big Picture first, rules second: `collect-events` names every event before `attach-event-rules` asks what must
hold for each one — the same "map everything, then go deep" shape as `enumerate-test-cases` before `cover-batch`
in the `tdd` bundle, applied to modelling instead of testing.

## Protocols

**Enabled**

| No | Id                                                                   | Title                                             | Note    |
|----|----------------------------------------------------------------------|---------------------------------------------------|---------|
| 1  | [event-storming](protocols/event-storming/protocol.md)               | Event storming from a requirements input          |         |
| 2  | [collect-events](protocols/collect-events/protocol.md)               | Collect every domain event, Big Picture style     |         |
| 3  | [attach-event-rules](protocols/attach-event-rules/protocol.md)       | Attach the rules that must hold for each event    | repeats |
| 4  | [attach-rules-batch](protocols/attach-rules-batch/protocol.md)       | Attach rules for a batch of events                |         |
| 5  | [identify-aggregates](protocols/identify-aggregates/protocol.md)     | Group events under the aggregate that owns them   |         |
| 6  | [derive-commands](protocols/derive-commands/protocol.md)             | Derive the command that triggers each event       | notify  |
| 7  | [derive-views](protocols/derive-views/protocol.md)                   | Derive the read models the use cases will need    | notify  |
| 8  | [derive-use-cases](protocols/derive-use-cases/protocol.md)           | Derive use cases from command + aggregate + event | notify  |
| 9  | [draw-bounded-contexts](protocols/draw-bounded-contexts/protocol.md) | Draw bounded contexts and how they communicate    |         |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

None. Every rule this bundle applies while modelling belongs to `spec-writing` or stays fundament.

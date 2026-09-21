---
id: model-slice
title: Model one use-case slice, from rules to use case
description: >
  Models one slice — a single candidate use case — end to end: the rules for its events, the aggregate that owns
  them, the command that triggers them, the read models it needs, and the use case that ties those together. The
  events themselves were already collected for the whole input (the cheap, Big Picture pass); everything from the
  rules onward is done one slice at a time, so a developer can judge the direction on a complete example before
  the next slice starts, instead of after every event in the input has been through every step.
input: the current slice from event-model.md's `## Slices`, plus every event already collected
output: >
  the slice's events with their rules, its aggregate (new, or an earlier one extended or revised), its command(s),
  its view(s) and its use case, all confirmed and already written into event-model.md's sections
steps: [attach-event-rules, identify-aggregates, derive-commands, derive-views, derive-use-cases]
done-when: the slice's rules, aggregate, commands, views and use case are all confirmed
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [attach-event-rules](../attach-event-rules/protocol.md) — for this slice's events only; an event an earlier
   slice already attached rules to is not asked about again.
2. [identify-aggregates](../identify-aggregates/protocol.md) — place this slice's events under an aggregate,
   checking invariants against every collected event and every aggregate decided so far, not only this slice.
3. [derive-commands](../derive-commands/protocol.md)
4. [derive-views](../derive-views/protocol.md)
5. [derive-use-cases](../derive-use-cases/protocol.md) — confirms the slice's provisional use case as a real
   command / aggregate / event triple, and says so if that changes the slice list.

Every later slice can revise what an earlier one decided — most often an aggregate boundary. Such a revision is
always named as a revision, at the checkpoint of the step that makes it; never applied silently.

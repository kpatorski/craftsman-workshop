---
id: slice-loop
title: Take each slice from rules to working code, one at a time
description: >
  Runs one slice — one candidate use case — all the way through: modelling, a drafted spec, the use case
  implemented test-first, and a direction check on the finished result, then the next slice. Nobody builds a large
  system in one go, and nobody can hold every use case and event in their head; the unit of work is one use case,
  finished and committed, before the next one is even modelled. Lives in the fundament because it joins steps from
  three bundles (`event-storming`, `spec-writing` and the `implement` entry point's scenarios).
input: the ordered slice list in event-model.md's `## Slices`, confirmed by propose-candidate-specs
output: >
  every slice has its modelling in event-model.md, a reviewed spec in specs/, its use case implemented and
  committed, and a confirmed direction
steps: [model-slice, model-crud-slice, draft-spec, implement, confirm-direction]
repeat-until: every slice in event-model.md's `## Slices` is `done`
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

Repeat until the condition holds, always taking the first slice not yet `done`, in the confirmed order:

1. Model the slice — whichever alternative fits the `model` its entry in `## Slices` carries (each has its own
   `match`):
    - [model-slice](../../bundles/event-storming/protocols/model-slice/protocol.md) — `model: domain`.
    - [model-crud-slice](../model-crud-slice/protocol.md) — `model: crud`. If it finds a rule that is more than
      validation, the slice becomes `domain` and goes to `model-slice` instead.
2. [draft-spec](../../bundles/spec-writing/protocols/draft-spec/protocol.md)
3. [implement](../implement/protocol.md) — with the spec just drafted as its task. It chooses its own scenario: the
   first slice of a greenfield project is a bootstrap, a later one a new use case (a plain CRUD one has its own
   scenario), one that changes an aggregate an earlier slice already built is a change to existing code.
4. [confirm-direction](../confirm-direction/protocol.md)

Mark the slice `active` in `## Slices` when it starts. When `implement` finishes, record the spec's path and the
commit in that slice's entry; mark it `done` once its direction check is answered. This is the durable record of
where the run stands — a developer coming back to a large project reads it instead of remembering it. Standing
corrections recorded in `event-model.md`'s `## Direction` apply to every later slice, in the modelling and in the
code, and to a resumed session.

A slice ends at a resumable point: `done` in `## Slices`, code committed. The run can be cleared and resumed there
without losing anything.

---
id: slice-loop
title: Take each slice from rules to a reviewed spec, one at a time
description: >
  Runs one slice — one candidate use case — through modelling, spec drafting and a direction check, then the
  next slice. A slice is finished only when its spec is drafted and the developer has said whether the direction
  is right, so the first complete example reaches the developer while the remaining slices are still untouched.
  Lives in the fundament because it joins steps from two bundles (`event-storming` and `spec-writing`).
input: the ordered slice list in event-model.md's `## Slices`, confirmed by propose-candidate-specs
output: every slice has its modelling written to event-model.md, a reviewed spec in specs/, and a confirmed direction
steps: [model-slice, draft-spec, confirm-direction]
repeat-until: every slice in event-model.md's `## Slices` is `done`
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

Repeat until the condition holds, always taking the first slice not yet `done`, in the confirmed order:

1. [model-slice](../../bundles/event-storming/protocols/model-slice/protocol.md)
2. [draft-spec](../../bundles/spec-writing/protocols/draft-spec/protocol.md)
3. [confirm-direction](../confirm-direction/protocol.md)

Mark the slice `active` in `## Slices` when it starts and `done` when its direction check is answered. Standing
corrections recorded in `event-model.md`'s `## Direction` apply to every later slice, and to a resumed session.

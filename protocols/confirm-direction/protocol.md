---
id: confirm-direction
title: Confirm the direction on one finished slice
description: >
  Shows one finished slice as a whole — what was modelled and the spec drafted from it — and asks whether the
  approach is right before the next slice starts. The point is to find out at slice one, on one complete example,
  that the level of detail or the way aggregates are cut is wrong, rather than after every slice has been built
  the same way.
input: one slice's modelling in event-model.md and its drafted spec
output: >
  the developer's verdict on the direction — carried on, corrected (and recorded), or paused for implementation
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Slice <n> of <total> done: <use case name>.

    Events: <list>
    Rules: <each rule, one per line>
    Aggregate: <name>, protecting <invariant> <marked as a revision if it changed an earlier one>
    Command: <name>, rejectable: <failure outcomes> / unconditional
    View: <name and source>
    Spec: <path>, <k> acceptance criteria

    Is this the right direction for the remaining <total minus n> slices?
    1. Yes, continue in the same style
    2. Adjust the style — say what to change
    3. Pause — implement this spec first
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Show the slice compactly, straight from `event-model.md` and the spec — a summary, not a re-asking of the
   decisions already confirmed step by step.
2. **Continue** — mark the slice `done`; the loop takes the next one.
3. **Adjust** — the developer says what is wrong in general terms (rules too fine-grained, aggregate cut at the
   wrong level, spec too long). Redo this slice in that direction, and write the correction to `event-model.md`'s
   `## Direction` so every later slice — and a resumed session — applies it without being told again. Record it in
   the checkpoint log too.
4. **Pause** — mark the slice `done`, set the session's `Next` to "implement specs/NNN-…, then resume
   domain-design at slice <n+1>", and stop cleanly. `implement` and `domain-design` are separate sessions; this is
   the hand-off between them, not a new mechanism.
5. Disabling this protocol turns the stop off (see `core.md`, `checkpoint`) — the slices still run one at a time,
   the developer is just not asked between them.

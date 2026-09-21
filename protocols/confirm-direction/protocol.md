---
id: confirm-direction
title: Confirm the direction on one finished slice
description: >
  Shows one finished slice — modelled, specified and implemented — and where the whole run stands, and asks
  whether the approach is right before the next slice starts. Finding out on the first working use case that the
  level of detail or the way aggregates are cut is wrong is cheap; finding out after every slice has been built
  the same way is not.
input: one slice's modelling in event-model.md, its spec, and its implementation commit
output: >
  the developer's verdict on the direction — carried on, corrected (and recorded), or stopped here
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Slice <n> of <total> done: <use case name>.

    Built: <commit>, <k> tests green, <what the use case now does, in one line>
    Aggregate: <name>, protecting <invariant> <marked as a revision if it changed an earlier one>
    Spec: <path>, <k> acceptance criteria

    Progress: <n> of <total> done — <names>. Next: <name>.

    Is this the right direction for the remaining <total minus n> slices?
    1. Yes, continue in the same style
    2. Adjust the style — say what to change
    3. Stop here
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Show the slice compactly, straight from `event-model.md`, the spec and the commit — a summary, not a re-asking
   of decisions already confirmed step by step. The progress line is the point of it for a large project: what is
   done, what is next, without anyone having to remember.
2. **Continue** — mark the slice `done`; the loop takes the next one.
3. **Adjust** — the developer says what is wrong in general terms (rules too fine-grained, aggregate cut at the
   wrong level, tests too thin, code structured wrongly). Redo this slice in that direction, and write the
   correction to `event-model.md`'s `## Direction` so every later slice — and a resumed session — applies it
   without being told again. Record it in the checkpoint log too.
4. **Stop here** — mark the slice `done` and set the session's `Next` to the next slice, so the run resumes from
   exactly here.
5. Disabling this protocol turns the stop off (see `core.md`, `checkpoint`) — the slices still run one at a time,
   the developer is just not asked between them.

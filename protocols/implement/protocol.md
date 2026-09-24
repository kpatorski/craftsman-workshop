---
id: implement
title: Drive a coding task in a HUMAN <-> AI loop
description: >
  Entry point for turning one defined task — a spec, or a task description on its own — into working code. Never a large
  generated drop: advances in small, checkpoint-gated moves, following whichever of the scenarios below actually fits
  the task.
input: a task description or a spec file, plus optionally `style=<name|path>` and `session=<path>`
output: a green, refactored suite and production code, or a session left `blocked`/`active` with a clear `Next`
entry-point: true
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read the task. Check each alternative below's `match` against it, in order, and run the first one that fits:
    - [scenario-new-crud-use-case](../scenario-new-crud-use-case/protocol.md) — a new use case whose spec states
      `Model: crud`. Checked before the one below, which would otherwise also fit.
    - [scenario-new-use-case](../scenario-new-use-case/protocol.md) — a new use case in a module that already has some.
    - [scenario-change-existing-code](../scenario-change-existing-code/protocol.md) — changing behaviour that already
      has tests.
    - [scenario-utils](../scenario-utils/protocol.md) — a genuine shared utility.
    - [scenario-missing-tests](../../bundles/legacy-code/protocols/scenario-missing-tests/protocol.md) — covering
      existing, untested, working code.
    - [scenario-bootstrap-module](../../bundles/module-bootstrap/protocols/scenario-bootstrap-module/protocol.md) — a
      greenfield module.
2. If none fits cleanly, say so and ask the developer whether to proceed with the closest one or stop — never invent a
   process none of them describe.
3. Everything past this point — loading the enabled directives an inner step's `applies-when` calls for, opening or
   resuming the per-task session file, walking the chosen scenario's steps, honouring every checkpoint — is the
   execution mechanics described in the `craftsman` skill itself, not repeated per protocol.
4. When this protocol runs as a step of another one — [slice-loop](../slice-loop/protocol.md) does this for every
   slice — it runs inside the caller's session: no session file of its own, its steps nest under the caller's in
   the one Call stack, and its checkpoints stop exactly as they would if `implement` had been invoked directly.

## Examples

"Add a `CancelReservation` use case to the booking module" matches `scenario-new-use-case`. "Add
`RenameExerciseCategory`", with a spec stating `Model: crud`, matches `scenario-new-crud-use-case`. "Cover the
`PricingCalculator` class, which works but has no tests" matches `scenario-missing-tests`.

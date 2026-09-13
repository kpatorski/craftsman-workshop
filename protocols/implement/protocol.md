---
id: implement
title: Drive a coding task in a HUMAN <-> AI loop
description: >
  Entry point for turning one defined task — a spec, or a task description on its own — into working code. Never a large generated drop: advances in small, checkpoint-gated moves, following whichever of the scenarios below actually fits the task. Migrated from the `developer` skill's `SKILL.md`.
input: a task description or a spec file, plus optionally `style=<name|path>` and `session=<path>`
output: a green, refactored suite and production code, or a session left `blocked`/`active` with a clear `Next`
entry-point: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Read the task. Check each alternative below's `match` against it, in order, and run the first one that fits:
   - [scenario-new-use-case](../scenario-new-use-case/protocol.md) — a new use case in a module that already has some.
   - [scenario-change-existing-code](../scenario-change-existing-code/protocol.md) — changing behaviour that already has tests.
   - [scenario-utils](../scenario-utils/protocol.md) — a genuine shared utility.
   - [scenario-missing-tests](../scenario-missing-tests/protocol.md) — covering existing, untested, working code.
   - [scenario-bootstrap-module](../scenario-bootstrap-module/protocol.md) — a greenfield module.
2. If none fits cleanly, say so and ask the developer whether to proceed with the closest one or stop — never invent a process none of them describe.
3. Everything past this point — loading the enabled directives an inner step's `applies-when` calls for, opening or resuming the per-task session file, walking the chosen scenario's steps, honouring every checkpoint — is the execution mechanics described in the `craftsman` skill itself, not repeated per protocol.

## Examples

"Add a `CancelReservation` use case to the booking module" matches `scenario-new-use-case`. "Cover the `PricingCalculator` class, which works but has no tests" matches `scenario-missing-tests`.

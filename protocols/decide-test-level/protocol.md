---
id: decide-test-level
title: Decide how high to test this
description: >
  Before scaffolding, decide the level the behaviour is tested at, using the how-high-to-test directive. Default is high / black-box through a package entry point; go lower only when that directive's reasons apply.
input: the behaviour to be tested and its target module
output: the chosen test level and the target entry point for the suite
uses: [how-high-to-test]
checkpoint:
  type: ask
  blocking: true
  when: the level is not already fixed by an existing suite or obvious from the target class
  prompt: >
    I'd test this at <level> through <entry point>, because <reason>. Does that match how you'd frame it?
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Consult [how-high-to-test](../../directives/how-high-to-test/directive.md) for the level and the reasoning; state both
at the checkpoint above.

Used
by: [tdd-loop](../tdd-loop/protocol.md), [characterize-loop](../characterize-loop/protocol.md). [scenario-utils](../scenario-utils/protocol.md)
overrides it — forced to `util-unit-suite`, no checkpoint.

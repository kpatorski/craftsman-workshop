---
id: check-coverage
title: Check the target is covered before changing it
description: >
  Before changing behaviour, check whether the code path is under test.
input: the target class or method to be changed
output: a decision on how to proceed when coverage is missing
checkpoint:
  type: ask
  blocking: true
  when: the target code path is not covered by tests
  prompt: >
    <path> isn't covered. Add characterization tests first (separate commit), or go straight into the change?
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [scenario-change-existing-code](../scenario-change-existing-code/protocol.md).

---
id: check-coverage
title: Check the target is covered before changing it
description: >
  Checks the target is covered by tests before changing it.
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

1. Before changing behaviour, check whether the code path is under test.
2. If it is not covered, stop at the checkpoint below.

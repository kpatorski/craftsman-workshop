---
id: finish-loop
title: Close the loop
description: >
  Closes the TDD loop and confirms what happens next.
input: the refactored, green suite and production code
output: a closed tdd-loop run, with the developer's decision on what happens next
checkpoint:
  type: ask
  blocking: true
  shows: [file-list, full-diff]
  prompt: "Use case done: <summary>. Whole suite green. Commit it, or more changes first?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Show what was produced — new files, the test list, the whole diff.
2. Confirm the procedure's `done-when` holds.
3. Ask what happens next.

Used by: [tdd-loop](../tdd-loop/protocol.md).

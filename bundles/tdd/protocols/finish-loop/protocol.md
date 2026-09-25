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
  prompt: >
    Use case done: <summary>. Directive check: <no violations, or what was fixed>. Whole suite green.
    Commit it, or more changes first?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Check the whole diff, tests and production code, against every directive that is enabled and whose `applies-when`
   matches the change — not only the ones already loaded this run. Read each such directive again and compare it to
   the diff line by line; do not rely on having followed it while writing. Fix every violation, re-run the suite,
   and only then continue. Name each fix in the checkpoint.
2. Show what was produced — new files, the test list, the whole diff.
3. Confirm the procedure's `done-when` holds.
4. Ask what happens next.

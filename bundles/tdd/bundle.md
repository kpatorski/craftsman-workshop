---
id: tdd
title: Test-first implementation loop
requires: [ testing ]
description: >
  The red-green-refactor loop: decide how deep to test, scaffold the suite, enumerate every known case as a
  failing stub, implement in small batches with a design-direction checkpoint between them, then refactor tests
  and production code separately.
---

## Schema

No fields of its own — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Bundle

Input is a behaviour to build, in an already-located target. Output is a green suite, tests and production code
both refactored. `requires: [testing]` because every stub `enumerate-test-cases` writes and every batch
`cover-batch` implements must already satisfy the suite-shape rules — this bundle drives the suite, `testing`
states what it must look like.

Big Picture first, one case at a time second: `enumerate-test-cases` lists every known case as a stub before
`cover-batch` implements any of them — the same "map everything, then go deep" shape as `collect-events` before
`attach-event-rules` in the `event-storming` bundle, applied to testing instead of modelling.

## Protocols

**Enabled**

| No | Id                                                                       | Title                                                     | Note    |
|----|--------------------------------------------------------------------------|-----------------------------------------------------------|---------|
| 1  | [tdd-loop](protocols/tdd-loop/protocol.md)                               | Test-first implementation loop                            |         |
| 2  | [decide-test-level](protocols/decide-test-level/protocol.md)             | Decide how high to test this                              |         |
| 3  | [scaffold-suite](protocols/scaffold-suite/protocol.md)                   | Create the empty test suite                               |         |
| 4  | [enumerate-test-cases](protocols/enumerate-test-cases/protocol.md)       | List every known test case as a failing stub              |         |
| 5  | [cover-cycle](protocols/cover-cycle/protocol.md)                         | Batch coverage cycle                                      | repeats |
| 6  | [cover-batch](protocols/cover-batch/protocol.md)                         | Implement bodies for a small batch of stubs               |         |
| 7  | [minimal-production-code](protocols/minimal-production-code/protocol.md) | Write the least production code that makes the batch pass |         |
| 8  | [review-design-direction](protocols/review-design-direction/protocol.md) | Confirm the design direction before the next batch        |         |
| 9  | [snapshot-green](protocols/snapshot-green/protocol.md)                   | Snapshot the green suite before refactoring               |         |
| 10 | [refactor-tests](protocols/refactor-tests/protocol.md)                   | Refactor the tests first                                  |         |
| 11 | [refactor-production](protocols/refactor-production/protocol.md)         | Refactor the production code                              |         |
| 12 | [finish-loop](protocols/finish-loop/protocol.md)                         | Close the loop                                            |         |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

None. Every rule this bundle applies while writing tests belongs to `testing`; every rule it applies while writing
production code stays fundament (`production-code` and everything it composes).

---
id: tdd-loop
title: Test-first implementation loop
description: >
  The loop to run whenever behaviour is added or changed. Not "write all tests, then all code" — it advances in small
  batches, and the design direction is confirmed with the developer before it hardens. Cases found mid-loop are captured
  as stubs at once.
input: a behaviour to build, in a located target
output: a green suite, tests and production code both refactored
steps: [decide-test-level, scaffold-suite, enumerate-test-cases, cover-cycle, snapshot-green, refactor-tests,
  refactor-production, finish-loop]
done-when: the whole suite is green and both tests and production code are refactored
---

## Schema

Introduces no new fields — see `core.md`. `cover-cycle` is itself a
protocol with `repeat-until` — nesting goes as deep as the process does.

## Protocol

1. [decide-test-level](../decide-test-level/protocol.md)
2. [scaffold-suite](../scaffold-suite/protocol.md)
3. [enumerate-test-cases](../enumerate-test-cases/protocol.md)
4. [cover-cycle](../cover-cycle/protocol.md)
5. [snapshot-green](../snapshot-green/protocol.md)
6. [refactor-tests](../refactor-tests/protocol.md)
7. [refactor-production](../refactor-production/protocol.md)
8. [finish-loop](../finish-loop/protocol.md)

A case discovered mid-loop is added as a stub immediately and the current step continues — that is the loop working, not
a derailment.

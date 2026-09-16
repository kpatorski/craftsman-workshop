---
id: scenario-new-use-case
title: Add a new use case to an existing module
description: >
  A module whose bounded contexts, business rules and communication style (events, ports & adapters) are already
  decided; event storming is done. The new use case usually mirrors the structure of existing ones, but may introduce
  its own convention if it genuinely needs to.
input: a module that already has at least one use case, and the new use case's business rules
output: same as tdd-loop's output — a green, refactored suite and production code for the new use case
match: task is to add or implement a new use case in a module that already has some
steps: [locate-target, confirm-conventions, create-empty-package, tdd-loop]
done-when: tdd-loop's done-when holds
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [locate-target](../locate-target/protocol.md) — find the module to work in.
2. [confirm-conventions](../confirm-conventions/protocol.md) — settle placement and naming before creating anything.
3. [create-empty-package](../create-empty-package/protocol.md) — create the empty target package.
4. [tdd-loop](../../bundles/tdd/protocols/tdd-loop/protocol.md) — build the use case test-first.

---
id: bootstrap-module
title: Module bootstrap
description: >
  Sets up a new module from nothing — stack, build, package skeleton, baseline configuration — and ends ready to build
  its first use case.
input: a decision to start a new module, and the output of domain-design if one exists
output: a compiling module, an empty test running, and the first aggregate chosen — ready for scenario-new-use-case
steps: [choose-stack, create-build, add-dependencies, scaffold-package-skeleton, base-configuration,
  pick-first-aggregate]
done-when: the module compiles, an empty test runs, and the first aggregate is chosen — ready for scenario-new-use-case
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [choose-stack](../choose-stack/protocol.md)
2. [create-build](../create-build/protocol.md)
3. [add-dependencies](../add-dependencies/protocol.md)
4. [scaffold-package-skeleton](../scaffold-package-skeleton/protocol.md)
5. [base-configuration](../base-configuration/protocol.md)
6. [pick-first-aggregate](../pick-first-aggregate/protocol.md)

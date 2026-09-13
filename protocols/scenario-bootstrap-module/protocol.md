---
id: scenario-bootstrap-module
title: Found a new project or module
description: >
  A greenfield module. No sibling use cases to mirror, so structural decisions are made explicitly against the architecture-profile directive. Ends by handing the first aggregate's case to scenario-new-use-case.
input: a decision to start a new project or module, and the output of domain-design (events, aggregates)
output: a compiling, runnable module with baseline configuration and its first aggregate chosen
match: task is to start a new project or module from nothing
steps: [bootstrap-module]
done-when: bootstrap-module's done-when holds
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. [bootstrap-module](../bootstrap-module/protocol.md) — set up the module from nothing, then hand off the first aggregate's use case to [scenario-new-use-case](../scenario-new-use-case/protocol.md).

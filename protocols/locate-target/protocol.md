---
id: locate-target
title: Locate the module / package / class to work in
description: >
  Find where the work belongs before touching anything. For a new use case this is the package to create; for a change it is the existing class and its suite.
input: the task description
output: the target package and, for changes, the existing test file(s)
checkpoint:
  type: ask
  blocking: true
  prompt: "I'll work in <path>. Right place?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [scenario-new-use-case](../scenario-new-use-case/protocol.md), [scenario-change-existing-code](../scenario-change-existing-code/protocol.md), [scenario-utils](../scenario-utils/protocol.md).

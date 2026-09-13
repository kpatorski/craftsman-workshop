---
id: locate-target
title: Locate the module / package / class to work in
description: >
  Locates the module, package, or class to work in, before touching anything.
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

1. For a new use case, find the package to create.
2. For a change, find the existing class and its suite.

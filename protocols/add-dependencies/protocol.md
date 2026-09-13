---
id: add-dependencies
title: Add the agreed dependencies
description: >
  Adds the dependencies choose-stack agreed on, nothing more.
input: the stack agreed by choose-stack
output: resolved dependencies, project still compiles
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Add only the dependencies choose-stack agreed, each at its latest stable version.
2. No speculative dependencies — nothing not explicitly agreed.

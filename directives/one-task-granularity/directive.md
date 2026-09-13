---
id: one-task-granularity
title: One spec is one thing a single implement run can finish
description: >
  Keeps a spec small enough that `implement` can carry it through in one go, without hitting its own architecture decision mid-way.
applies-when: proposing or reviewing a candidate spec
precedence: none — this always applies
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- a spec covers one coherent change; if it needs its own architecture decision or spans bounded contexts, split it
- merging use cases into one spec is proposed explicitly at `propose-candidate-specs` — never silent

## Examples

Two small use cases on the same aggregate (`assign-role` / `revoke-role`) may merge into one spec; a use case touching two bounded contexts must split into two.

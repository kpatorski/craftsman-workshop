---
id: enumerate-cases-from-code
title: Read the code to list the cases it already handles
description: >
  Derive the test cases from the existing implementation — branches, guards, edge values — not from requirements. Each becomes a failing stub.
input: existing, untested code
output: one failing stub per observed behaviour path
checkpoint:
  type: ask
  blocking: true
  prompt: "Cases I read out of the code: <list>. Missing any path?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [characterize-loop](../characterize-loop/protocol.md).

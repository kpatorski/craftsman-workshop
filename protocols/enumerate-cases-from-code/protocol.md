---
id: enumerate-cases-from-code
title: Read the code to list the cases it already handles
description: >
  Reads existing code to list the cases it already handles, one failing stub per case.
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

1. Derive the test cases from the existing implementation — branches, guards, edge values — not from requirements.
2. Write each as a failing stub.

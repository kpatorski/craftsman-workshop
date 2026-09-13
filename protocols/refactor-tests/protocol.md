---
id: refactor-tests
title: Refactor the tests first
description: >
  Assess the suite before the production code. Simplify methods, extract intent-revealing helpers, introduce fixtures where the same complex object is built repeatedly. Tests stay green throughout.
input: the green suite snapshotted by snapshot-green
output: a suite that reads as prose, still green
uses: [how-high-to-test]
checkpoint:
  type: ask
  blocking: true
  shows: [test-diff]
  prompt: "Tests after refactor — diff. Move on to the production code?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [tdd-loop](../tdd-loop/protocol.md).

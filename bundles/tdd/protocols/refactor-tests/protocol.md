---
id: refactor-tests
title: Refactor the tests first
description: >
  Refactors the tests first, before touching production code.
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

Introduces no new fields — see `core.md`.

## Protocol

1. Simplify methods, extract intent-revealing helpers.
2. Introduce fixtures where the same complex object is built repeatedly.
3. Keep the tests green throughout.

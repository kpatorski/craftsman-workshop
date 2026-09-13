---
id: characterize-batch
title: Lock in current behaviour for a small batch
description: >
  Locks in current behaviour for a small batch of stubs.
input: a batch of stubs from enumerate-cases-from-code
output: passing characterization tests for the batch
uses: [stub-vs-in-memory]
checkpoint:
  type: ask
  blocking: true
  shows: [test-diff]
  prompt: "Batch locked in. Continue?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. For 2-3 stubs, run the existing code and observe what it actually does.
2. Write an assertion that captures that — the test asserts current behaviour, not desired behaviour.
3. If the current behaviour looks wrong, note it; do not fix it here.

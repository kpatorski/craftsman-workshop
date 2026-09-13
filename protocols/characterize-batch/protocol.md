---
id: characterize-batch
title: Lock in current behaviour for a small batch
description: >
  For 2-3 stubs, run the existing code, observe what it actually does, and write an assertion that captures that. The test asserts current behaviour, not desired behaviour — if the current behaviour looks wrong, note it, do not fix it here.
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

Used by: [characterize-cycle](../characterize-cycle/protocol.md).

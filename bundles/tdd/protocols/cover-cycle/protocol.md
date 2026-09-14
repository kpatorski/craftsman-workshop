---
id: cover-cycle
title: Batch coverage cycle
description: >
  Each iteration covers a small batch of stubs and stops for the developer's go-ahead before the next one. A stub discovered mid-iteration is added immediately, then the current iteration continues.
input: the stub list from enumerate-test-cases
output: every stub from enumerate-test-cases has a passing body
steps: [cover-batch, minimal-production-code, review-design-direction]
repeat-until: every stub from enumerate-test-cases has a passing body
---

## Schema

Introduces no new fields — see `core.md`. Replaces the old `loop`
kind —
see `repeat-until`.

## Protocol

Repeat until the condition holds:

1. [cover-batch](../cover-batch/protocol.md)
2. [minimal-production-code](../minimal-production-code/protocol.md)
3. [review-design-direction](../review-design-direction/protocol.md)

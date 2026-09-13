---
id: characterize-cycle
title: Characterization batch cycle
description: >
  Each iteration locks in current behaviour for a small batch of stubs, then stops for the developer's go-ahead before the next one.
input: the stub list from enumerate-cases-from-code
output: every stub from enumerate-cases-from-code has a passing body
steps: [characterize-batch]
repeat-until: every stub from enumerate-cases-from-code has a passing body
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md). Replaces the old `loop` kind —
see `repeat-until`.

## Protocol

Repeat until the condition holds:

1. [characterize-batch](../characterize-batch/protocol.md)

---
id: extract-rules
title: Extract rules section by section
description: >
  Each iteration extracts the Given/When/Then rules for one section and stops for confirmation before the next.
input: sections identified by read-input
output: every section of the input has its rules extracted and confirmed
steps: [extract-rules-batch]
repeat-until: every section of the input has its rules extracted and confirmed
---

## Schema

Introduces no new fields — see `core.md`. Replaces the old `loop` kind — see `repeat-until`.

## Protocol

Repeat until the condition holds:

1. [extract-rules-batch](../extract-rules-batch/protocol.md)

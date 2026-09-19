---
id: extract-rules
title: Extract rules section by section
description: >
  Each iteration extracts one section's candidate rules, then triages them — a cited candidate is written, an
  uncited one stops for the developer — before moving to the next section.
input: sections identified by read-input
output: every section of the input has its rules extracted, triaged, and either written or resolved
steps: [extract-rules-batch, triage-rules-batch]
repeat-until: every section of the input has its rules extracted, triaged, and either written or resolved
---

## Schema

Introduces no new fields — see `core.md`. Replaces the old `loop` kind — see `repeat-until`.

## Protocol

Repeat until the condition holds:

1. [extract-rules-batch](../extract-rules-batch/protocol.md)
2. [triage-rules-batch](../triage-rules-batch/protocol.md)

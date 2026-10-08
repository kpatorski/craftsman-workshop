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

**A long input is read in parallel, and still decided one section at a time.** Extraction is phrasing, not
judgement, and one section's candidates do not depend on another's — so when the input has more than three
sections, step 1 runs for all of them at once as delegated read-only preparation (`EXECUTION.md`, same name): one
helper per section, each given [extract-rules-batch](../extract-rules-batch/protocol.md) as its rules. Each helper
returns, per candidate: the section, the Given/When/Then, the sentence of the input it was drawn from, quoted, and
any statement in that section of who benefits and how, quoted — or `NOT FOUND`. It also returns what it left out as
not Given/When/Then material.

Step 2 is never delegated. Triage runs here, section by section in the input's order, exactly as written: a quoted
benefit is checked against [triage-rules-batch](../triage-rules-batch/protocol.md)'s own tests before it counts as
a citation, cited candidates are written in that turn, and uncited ones stop for the developer.

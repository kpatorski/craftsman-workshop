---
id: finalize-digest
title: Write the rules file
description: >
  Writes the confirmed rules to business-rules.md and closes the run. Named `finalize-digest`, not `finalize` — that id was already taken by `domain-design`'s own closing step; see the `craftsman` plan, R5.
input: all confirmed rules from extract-rules
output: business-rules.md, grouped by section
checkpoint:
  type: ask
  blocking: true
  prompt: "Digest done: <n> rules across <m> sections, written to business-rules.md. Anything to fix?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Write all confirmed rules to business-rules.md, grouped by section.
2. Each rule as its own structured block, ready for any downstream reader (a human, `domain-design`, or anything else)
   to consume.

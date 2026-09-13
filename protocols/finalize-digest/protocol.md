---
id: finalize-digest
title: Write the rules file
description: >
  Write all confirmed rules to business-rules.md, grouped by section, each rule as its own structured block — ready for any downstream reader (a human, `domain-design`, or anything else) to consume. Named `finalize-digest`, not `finalize` — `domain-design`'s own closing step already holds that id; see the `craftsman` plan, R5.
input: all confirmed rules from extract-rules
output: business-rules.md, grouped by section
checkpoint:
  type: ask
  blocking: true
  prompt: "Digest done: <n> rules across <m> sections, written to business-rules.md. Anything to fix?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [digest-requirements](../digest-requirements/protocol.md).

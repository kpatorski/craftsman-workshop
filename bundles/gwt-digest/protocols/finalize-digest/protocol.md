---
id: finalize-digest
title: Close the digest run
description: >
  Confirms business-rules.md holds every confirmed section's rules — each was already appended as it was
  confirmed, see extract-rules-batch — and closes the run. Named `finalize-digest`, not `finalize` — that id was
  already taken by `domain-design`'s own closing step; see the `craftsman` plan, R5.
input: all confirmed rules from extract-rules, already appended to business-rules.md batch by batch
output: business-rules.md confirmed complete, a closed digest run
checkpoint:
  type: ask
  blocking: true
  prompt: "Digest done: <n> rules across <m> sections, all in business-rules.md. Anything to fix?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read business-rules.md back and confirm every confirmed section's rules are actually present — a check, not a
   write. `extract-rules-batch` already wrote each section's rules as it was confirmed; this is not a second
   place the file gets built from.
2. If a section is missing (a batch's write was somehow skipped), write it now and say so explicitly — this
   should not happen when `extract-rules-batch` was followed, but the check exists so a gap is caught here, not
   discovered later by a downstream reader.

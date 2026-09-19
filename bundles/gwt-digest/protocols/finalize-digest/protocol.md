---
id: finalize-digest
title: Close the digest run
description: >
  Confirms business-rules.md holds every cited section's rules, and open-questions.md holds every parked one —
  each was already appended as it was resolved, see triage-rules-batch — and closes the run. Named
  `finalize-digest`, not `finalize` — that id was already taken by `domain-design`'s own closing step; see the
  `craftsman` plan, R5.
input: >
  all cited rules and all parked questions from extract-rules, already appended to business-rules.md and
  open-questions.md batch by batch
output: business-rules.md and open-questions.md confirmed complete, a closed digest run
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Digest done: <n> rules in business-rules.md, <m> open questions in open-questions.md, across <k> sections.
    Anything to fix?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read business-rules.md and, if it exists, open-questions.md back and confirm every resolved candidate is
   actually present in one or the other — a check, not a write. `triage-rules-batch` already wrote each
   candidate's resolution as it happened; this is not a second place either file gets built from.
2. If a candidate is missing from both (a batch's write was somehow skipped), write it to the correct file now
   and say so explicitly — this should not happen when `triage-rules-batch` was followed, but the check exists
   so a gap is caught here, not discovered later by a downstream reader.

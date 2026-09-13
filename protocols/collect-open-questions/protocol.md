---
id: collect-open-questions
title: Surface every unresolved open question
description: >
  Gather Open questions across all drafted specs and present them together, rather than leaving them hidden inside individual files. An answer folds back into the relevant spec and clears its `status: blocked` if that was the only blocker.
input: every spec drafted by detail-spec
output: every remaining open question resolved, or explicitly left open with the spec marked blocked
checkpoint:
  type: ask
  blocking: true
  prompt: "Open questions across all specs: <list>. Any you can resolve now?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [requirements-analysis](../requirements-analysis/protocol.md).

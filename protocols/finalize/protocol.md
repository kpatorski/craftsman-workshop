---
id: finalize
title: Write the specs and close the run
description: >
  Ensure every spec file is saved, write or update specs/README.md as an index (id, title, status, shape), summarise, and set the session's Next.
input: all reviewed specs and their resolved open questions
output: specs/ written to disk, specs/README.md current, a session ready to close or continue
checkpoint:
  type: ask
  blocking: true
  shows: [file-list]
  prompt: "Analysis done: <n> specs written to specs/. Anything to add before we stop?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). Reserved id — the `analyse`
workshop's own closing step will need a different one; see the `craftsman` plan, R5.

## Protocol

Used by: [requirements-analysis](../requirements-analysis/protocol.md).

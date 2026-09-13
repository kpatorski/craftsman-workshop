---
id: finalize
title: Write the specs and close the run
description: >
  Writes every spec file, updates the index, and closes the run.
input: all reviewed specs and their resolved open questions
output: specs/ written to disk, specs/README.md current, a session ready to close or continue
checkpoint:
  type: ask
  blocking: true
  shows: [file-list]
  prompt: "Analysis done: <n> specs written to specs/. Anything to add before we stop?"
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md). Reserved id — the `analyse`
workshop's own closing step will need a different one; see the `craftsman` plan, R5.

## Protocol

1. Ensure every spec file is saved.
2. Write or update specs/README.md as an index — id, title, status, shape.
3. Summarise what was produced and set the session's Next.

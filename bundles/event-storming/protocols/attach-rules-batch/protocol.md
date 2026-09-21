---
id: attach-rules-batch
title: Attach rules for a batch of events
description: >
  Attaches the rules for one batch of events, confirms them, and updates event-model.md immediately — never
  deferred to the end of the loop. Found live in the sibling `gwt-digest` bundle's identical `extract-rules-batch`
  (same shape, same fix): a many-batch run left every confirmed rule sitting only in the session file (gitignored,
  see EXECUTION.md) until the very last step, so a developer watching the run had nothing real to read for the
  whole thing — "work done, invisible on disk".
input: a batch of the current slice's events from collect-events
output: precondition phrases (or attached rule ids) for the events in this batch, already written to event-model.md
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Rules attached, batch <n>:

    - <event>: <phrases>
    - <event>: <phrases>

    (one line per event, never joined into one paragraph — see EXECUTION.md, "Checkpoint protocol")

    Continue to the next batch, or adjust?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. For a small batch of events, attach the digested rule (s) that produced each.
2. If no digested rules exist, write the precondition phrases directly instead.
3. Stop and confirm before moving to the next batch.
4. **Once confirmed, update event-model.md in the same turn** — each event in this batch gets its attached rules
   recorded under it, in `event-model.md`'s `## Events` section (created by `collect-events`). Never accumulate
   several batches in memory before writing.

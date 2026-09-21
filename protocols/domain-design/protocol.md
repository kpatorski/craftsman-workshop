---
id: domain-design
title: Turn a requirements input into specs and working code, one use case at a time
description: >
  Entry point for the developer's own event-storming method, run in a HUMAN <-> AI loop. Takes a raw requirements input
  and, if present, a `business-rules.md` (from `analyse`, or written by hand) with Given/When/Then rules already
  extracted — authoritative when present, but not a hard dependency. Collects every event first, then takes one use
  case at a time from its rules to a reviewed spec to implemented, committed code, so the approach is judged on the
  first working example and no one has to keep the whole system in their head. There is only ever one path here,
  nothing to dispatch between.
input: >
  a requirements input (file, URL, or inline text), plus optionally `business-rules.md` and `style=<name|path>` /
  `session=<path>`
output: >
  `specs/NNN-slug.md` files plus a current `specs/README.md` index, and each spec's use case implemented and
  committed
entry-point: true
steps: [ingest, requirements-analysis]
done-when: requirements-analysis's done-when holds
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [ingest](../ingest/protocol.md) — read the input and any `business-rules.md`.
2. [requirements-analysis](../requirements-analysis/protocol.md) — every event first, then one use case at a time:
   model it, spec it, implement it.

Session file handling, directive loading, and resuming are the execution mechanics described in the `craftsman` skill
itself, not repeated per protocol — see [implement](../implement/protocol.md) for the same note.

---
id: domain-design
title: Turn a requirements input into reviewed, written task specs
description: >
  Entry point for the developer's own event-storming method, run in a HUMAN <-> AI loop. Takes a raw requirements input and, if present, a `business-rules.md` (from `analyse`, or written by hand) with Given/When/Then rules already extracted — authoritative when present, but not a hard dependency. Migrated from the `analyst` skill's `SKILL.md` and its single `scenario-analyze-input`, retired here as a separate file because there was only ever one path — nothing to dispatch between.
input: "a requirements input (file, URL, or inline text), plus optionally `business-rules.md` and `style=<name|path>` / `session=<path>`"
output: "`specs/NNN-slug.md` files plus a current `specs/README.md` index"
entry-point: true
steps: [ingest, requirements-analysis]
done-when: requirements-analysis's done-when holds
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. [ingest](../ingest/protocol.md) — read the input and any `business-rules.md`.
2. [requirements-analysis](../requirements-analysis/protocol.md) — event storming, then one spec per accepted candidate.

Session file handling, directive loading, and resuming are the execution mechanics described in the `craftsman` skill
itself, not repeated per protocol — see [implement](../implement/protocol.md) for the same note.

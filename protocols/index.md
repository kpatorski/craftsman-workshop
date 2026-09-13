---
name: protocols-index
description: >
  Lookup table for every protocol in this workshop — what order to work in, and where to stop.
  craftsman dispatches a task to an `entry-point` protocol found here, then walks its `steps`.
---

## Schema

No fields of its own beyond `Sources` below. `checkpoint`, `input`, `output`, `steps`, `repeat-until`, `done-when`,
`entry-point` are defined once in [core.md](../../craftsman/plugins/craftsman/core.md) — every protocol's own
`## Schema` section links back there instead of repeating the definition.

## Sources

Where installed protocols came from. `craftsman install <uri>` appends a row here and materializes the files under a
category directory below.

| Name     | Location        | Kind  |
|----------|-----------------|-------|
| workshop | `.` (this repo) | local |

## Protocols

Grouped by category, one `##` section per topic. Each category has two tables: **Enabled** (callable) and **Disabled**
(installed, present, switched off). `craftsman list protocols` reads both; dispatch to an `entry-point` reads only
Enabled.

Rebuild into a two-level index (this file linking to `index-<category>.md`) once any single category passes ~200
entries — same restraint as `core.md`'s golden rule, applied to structure instead of fields.

Categories are filled in during migration from `coding-style.md` / `spec-style.md` / `digest-style.md` (see the
`craftsman` plan, "Kolejność realizacji", step 3) — not invented ahead of the real content.

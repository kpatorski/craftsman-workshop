---
name: directives-index
description: >
  Lookup table for every directive in this workshop — what must be true about the code right now.
  A protocol step consults this to find and load directives whose `applies-when` matches its situation.
---

## Schema

No fields of its own beyond `Sources` below. `checkpoint`, `applies-when`, `precedence`, `enabled-by-default`,
`composes` are defined once in [core.md](../../craftsman/plugins/craftsman/core.md) — every directive's own `## Schema`
section links back there instead of repeating the definition.

## Sources

Where installed directives came from. `craftsman install <uri>` appends a row here and materializes the files under a
category directory below.

| Name     | Location        | Kind  |
|----------|-----------------|-------|
| workshop | `.` (this repo) | local |

## Directives

Grouped by category, one `##` section per topic. Each category has two tables: **Enabled** (what a protocol step
actually loads) and **Disabled** (installed, present, switched off). `craftsman list directives` reads both; a protocol
step loading directives for its `applies-when` reads only Enabled.

Rebuild into a two-level index (this file linking to `index-<category>.md`) once any single category passes ~200
entries — same restraint as `core.md`'s golden rule, applied to structure instead of fields.

Categories are filled in during migration from `coding-style.md` / `spec-style.md` / `digest-style.md` (see the
`craftsman` plan, "Kolejność realizacji", step 3) — not invented ahead of the real content.

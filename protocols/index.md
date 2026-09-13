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

Where installed protocols came from. `craftsman install <uri>` appends a row here and materializes each
protocol's files under `protocols/<id>/` — flat, not nested by category. Category grouping below is an index
concern only.

| Name     | Location        | Kind  |
|----------|-----------------|-------|
| workshop | `.` (this repo) | local |

## Examples

Applying [core.md](../../craftsman/plugins/craftsman/core.md)'s three-question test to real entries from this workshop:

- [`enumerate-test-cases`](../bundles/tdd/protocols/enumerate-test-cases/protocol.md) — "is this done yet?" is the
  only question that makes sense, not "is this true right now?"; it has a `checkpoint`, a clear start (an empty
  suite) and end (a full stub list); removing it changes what happens next in `tdd-loop`, not how any one piece of
  code looks. **Protocol.**
- [`tdd-loop`](../bundles/tdd/protocols/tdd-loop/protocol.md) — composes eight other protocols (`steps`), but
  composing is not the deciding factor (see core.md — both kinds nest). It is still a sequence with a start, an end
  (`done-when`), and steps that stop for checkpoints. **Protocol**, even though it is large.
- [`cover-cycle`](../bundles/tdd/protocols/cover-cycle/protocol.md) — repeats its steps until a condition holds
  (`repeat-until`). The old format had a separate `loop` kind for this; here it is an ordinary protocol, because the
  three-question test does not care whether a sequence runs once or several times — only whether it *is* a
  sequence.

The canonical borderline pair, from `core.md`:
[`decide-test-level`](../bundles/tdd/protocols/decide-test-level/protocol.md) (a *protocol* — it is a moment with a
checkpoint, part of a sequence) and
[`how-high-to-test`](../bundles/testing/directives/how-high-to-test/directive.md)
(a *directive* — the criteria that moment's decision must satisfy, true or not true independent of any sequence). Two
angles on the same concern, correctly split.

## Protocols

Grouped by category, one `##` section per topic. Each category has two tables: **Enabled** (callable) and **Disabled**
(installed, present, switched off). `craftsman list protocols` reads both; dispatch to an `entry-point` reads only
Enabled.

Rebuild into a two-level index (this file linking to `index-<category>.md`) once any single category passes ~200
entries — same restraint as `core.md`'s golden rule, applied to structure instead of fields.

### Implementation

Migrated from `coding-style.md` / the `developer` skill (batch 3 of 5). `implement` is the entry point (see plan
decision 7, formerly `/developer`); everything else is reached only through it or through a protocol it calls. Four
bundles now hold most of what used to be here — [tdd](../bundles/tdd/bundle.md),
[legacy-code](../bundles/legacy-code/bundle.md), [module-bootstrap](../bundles/module-bootstrap/bundle.md) — this
section keeps the entry point, the three scenarios that orchestrate across bundles (mostly fundament steps plus one
call into `tdd`, the same shape as `requirements-analysis`), and the shared steps several scenarios reuse.

**Enabled**

| No | Id                                                                         | Title                                                  | Note        |
|----|----------------------------------------------------------------------------|--------------------------------------------------------|-------------|
| 1  | [implement](implement/protocol.md)                                         | Drive a coding task in a HUMAN <-> AI loop             | entry point |
| 2  | [scenario-new-use-case](scenario-new-use-case/protocol.md)                 | Add a new use case to an existing module               |             |
| 3  | [scenario-change-existing-code](scenario-change-existing-code/protocol.md) | Change behaviour in existing code                      |             |
| 4  | [scenario-utils](scenario-utils/protocol.md)                               | Write or change a util                                 |             |
| 32 | [locate-target](locate-target/protocol.md)                                 | Locate the module / package / class to work in         | shared      |
| 33 | [create-empty-package](create-empty-package/protocol.md)                   | Create the empty target package                        |             |
| 34 | [challenge-the-util](challenge-the-util/protocol.md)                       | Confirm a util is really the right home                |             |
| 35 | [read-existing-tests](read-existing-tests/protocol.md)                     | Read the existing suite first                          |             |
| 36 | [check-coverage](check-coverage/protocol.md)                               | Check the target is covered before changing it         |             |
| 37 | [restate-current-behaviour](restate-current-behaviour/protocol.md)         | Restate what the code currently does                   |             |
| 38 | [confirm-conventions](confirm-conventions/protocol.md)                     | Confirm structural conventions before creating classes | shared      |

**Disabled**

Empty — nothing has been switched off yet. Populated by `craftsman disable protocol <id>`.

### Domain design

Migrated from `spec-style.md` / the `analyst` skill (batch 4 of 5). `domain-design` is the entry point (see plan
decision 7, formerly `/analyst`). Both the event-storming and spec-writing parts of this loop now live in their own
bundles — [event-storming](../bundles/event-storming/bundle.md) and
[spec-writing](../bundles/spec-writing/bundle.md) (decision 10). This section keeps only what is fundament: the
entry point, the orchestrator that calls into both bundles, and the two shared reading steps.

**Enabled**

| No | Id                                                         | Title                                                       | Note        |
|----|------------------------------------------------------------|-------------------------------------------------------------|-------------|
| 39 | [domain-design](domain-design/protocol.md)                 | Turn a requirements input into reviewed, written task specs | entry point |
| 40 | [requirements-analysis](requirements-analysis/protocol.md) | Requirements analysis loop                                  |             |
| 44 | [ingest](ingest/protocol.md)                               | Read the input                                              |             |
| 45 | [restate-understanding](restate-understanding/protocol.md) | Restate what needs to be done                               |             |

**Disabled**

Empty — nothing has been switched off yet.

### Analyse

Migrated from `digest-style.md` / the `digester` skill (batch 5 of 5, the smallest source file). `analyse` is the entry
point (see plan decision 7, formerly `/digester`). The GWT-extraction machinery this entry point drives now lives in
the [gwt-digest](../bundles/gwt-digest/bundle.md) bundle (decision 10) — this section keeps only what is fundament:
the entry point itself and the shared `read-input` step.

**Enabled**

| No | Id                                   | Title                                                     | Note        |
|----|--------------------------------------|-----------------------------------------------------------|-------------|
| 57 | [analyse](analyse/protocol.md)       | Turn raw requirements into Given/When/Then business rules | entry point |
| 60 | [read-input](read-input/protocol.md) | Read the input                                            |             |

**Disabled**

Empty — nothing has been switched off yet.

All migration batches complete (see the `craftsman` plan, "Kolejność realizacji", step 3). 62 protocols total.

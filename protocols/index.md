---
name: protocols-index
description: >
  Lookup table for every protocol in this workshop — what order to work in, and where to stop.
  craftsman dispatches a task to an `entry-point` protocol found here, then walks its `steps`.
---

## Schema

No fields of its own beyond `Sources` below. `checkpoint`, `input`, `output`, `steps`, `repeat-until`, `done-when`,
`entry-point` are defined once in `core.md` — every protocol's own
`## Schema` section links back there instead of repeating the definition.

## Sources

Where installed protocols came from. `craftsman install <uri>` appends a row here and materializes each
protocol's files under `protocols/<id>/` — flat, not nested by category. Category grouping below is an index
concern only. `Version` is the source's commit sha at last sync, when it is a git repository — re-run
`craftsman install <uri>` with the same URI any time to check whether it has moved on.

| Name     | Location        | Kind  | Version |
|----------|-----------------|-------|---------|
| workshop | `.` (this repo) | local | —       |

## Examples

Applying `core.md`'s three-question test to real entries from this workshop:

- [`enumerate-test-cases`](../bundles/tdd/protocols/enumerate-test-cases/protocol.md) — "is this done yet?" is the
  only question that makes sense, not "is this true right now?"; it has a `checkpoint`, a clear start (an empty
  suite) and end (a full stub list); removing it changes what happens next in `tdd-loop`, not how any one piece of
  code looks. **Protocol.**
- [`tdd-loop`](../bundles/tdd/protocols/tdd-loop/protocol.md) — composes eight other protocols (`steps`), but
  composing is not the deciding factor (see `core.md` — both kinds nest). It is still a sequence with a start, an end
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

`implement` is the entry point; everything else is reached only through it or through a protocol it calls. Three
bundles hold most of what implementation actually needs — [tdd](../bundles/tdd/bundle.md),
[legacy-code](../bundles/legacy-code/bundle.md), [module-bootstrap](../bundles/module-bootstrap/bundle.md) — this
section keeps the entry point, the three scenarios that orchestrate across bundles (mostly fundament steps plus one
call into `tdd`, the same shape as `requirements-analysis`), and the shared steps several scenarios reuse.

**Enabled**

| No | Id                                                                         | Title                                                  |
|----|----------------------------------------------------------------------------|--------------------------------------------------------|
| 1  | [implement](implement/protocol.md)                                         | Drive a coding task in a HUMAN <-> AI loop             |
| 2  | [scenario-new-use-case](scenario-new-use-case/protocol.md)                 | Add a new use case to an existing module               |
| 3  | [scenario-change-existing-code](scenario-change-existing-code/protocol.md) | Change behaviour in existing code                      |
| 4  | [scenario-utils](scenario-utils/protocol.md)                               | Write or change a util                                 |
| 32 | [locate-target](locate-target/protocol.md)                                 | Locate the module / package / class to work in         |
| 33 | [create-empty-package](create-empty-package/protocol.md)                   | Create the empty target package                        |
| 34 | [challenge-the-util](challenge-the-util/protocol.md)                       | Confirm a util is really the right home                |
| 35 | [read-existing-tests](read-existing-tests/protocol.md)                     | Read the existing suite first                          |
| 36 | [check-coverage](check-coverage/protocol.md)                               | Check the target is covered before changing it         |
| 37 | [restate-current-behaviour](restate-current-behaviour/protocol.md)         | Restate what the code currently does                   |
| 38 | [confirm-conventions](confirm-conventions/protocol.md)                     | Confirm structural conventions before creating classes |

**Disabled**

Empty — nothing has been switched off yet. Populated by `craftsman disable protocol <id>`.

### Domain design

`domain-design` is the entry point. Both the event-storming and spec-writing parts of this loop live in their own
bundles — [event-storming](../bundles/event-storming/bundle.md) and
[spec-writing](../bundles/spec-writing/bundle.md). This section keeps only what is fundament: the entry point, the
orchestrator that calls into both bundles, and the two shared reading steps.

**Enabled**

| No | Id                                                         | Title                                                                         |
|----|------------------------------------------------------------|-------------------------------------------------------------------------------|
| 39 | [domain-design](domain-design/protocol.md)                 | Turn a requirements input into specs and working code, one use case at a time |
| 40 | [requirements-analysis](requirements-analysis/protocol.md) | Requirements analysis loop                                                    |
| 41 | [ingest](ingest/protocol.md)                               | Read the input                                                                |
| 42 | [restate-understanding](restate-understanding/protocol.md) | Restate what needs to be done                                                 |
| 43 | [slice-loop](slice-loop/protocol.md)                       | Take each slice from rules to working code, one at a time                     |
| 44 | [confirm-direction](confirm-direction/protocol.md)         | Confirm the direction on one finished slice                                   |

**Disabled**

Empty — nothing has been switched off yet.

### Analyse

`analyse` is the entry point. The GWT-extraction machinery it drives lives in the
[gwt-digest](../bundles/gwt-digest/bundle.md) bundle — this section keeps only what is fundament: the entry point
itself and the shared `read-input` step.

**Enabled**

| No | Id                                   | Title                                                     |
|----|--------------------------------------|-----------------------------------------------------------|
| 57 | [analyse](analyse/protocol.md)       | Turn raw requirements into Given/When/Then business rules |
| 60 | [read-input](read-input/protocol.md) | Read the input                                            |

**Disabled**

Empty — nothing has been switched off yet.

64 protocols total.

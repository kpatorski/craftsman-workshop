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

Where installed directives came from. `craftsman install <uri>` appends a row here and materializes each directive's
files under `directives/<id>/` — flat, not nested by category. Category grouping below is an index concern only.

| Name     | Location        | Kind  |
|----------|-----------------|-------|
| workshop | `.` (this repo) | local |

## Examples

Applying [core.md](../../craftsman/plugins/craftsman/core.md)'s three-question test to real entries from this workshop:

- [`test-naming`](../bundles/testing/directives/test-naming/directive.md) — "is the test named by the state it describes?" has a yes/no answer at any
  moment; no checkpoint, no start or end; removing it changes how a test method's name looks, not what happens next.
  **Directive.**
- [`production-code`](production-code/directive.md) — composes 14 rules, but composing is not the deciding factor (see
  core.md — both kinds nest). It is still a yes/no check ("does this class follow the production-code rules?"), still no
  checkpoint. **Directive**, even though it is large.
- [`architecture-profile`](architecture-profile/directive.md) — started life as a `reference` in the old format (a block
  of settled facts, not a rule). It still passes the same test: "is the domain free of framework dependencies right
  now?" is a yes/no question about the present. **Directive.**

The canonical borderline pair, from `core.md`: [`decide-test-level`](../protocols/decide-test-level/protocol.md) (a
*protocol* — it is a moment with a checkpoint, part of a sequence) and
[`how-high-to-test`](../bundles/testing/directives/how-high-to-test/directive.md) (a *directive* — the criteria that
moment's decision must satisfy, true or not true independent of any sequence). Two angles on the same concern,
correctly split.

## Directives

Grouped by category, one `##` section per topic. Each category has two tables: **Enabled** (what a protocol step
actually loads) and **Disabled** (installed, present, switched off). `craftsman list directives` reads both; a protocol
step loading directives for its `applies-when` reads only Enabled.

Rebuild into a two-level index (this file linking to `index-<category>.md`) once any single category passes ~200
entries — same restraint as `core.md`'s golden rule, applied to structure instead of fields.

### Testing

Migrated from `coding-style.md`'s test-writing sections. Everything that used to be Enabled here now lives in the
[testing](../bundles/testing/bundle.md) bundle (decision 10) — this section keeps only the stack-specific `prefer-*`
toggles, standalone preferences that don't belong to any one theme.

**Enabled**

Empty — every entry that was here moved to the `testing` bundle.

**Disabled**

| No | Id                                                                            | Title                                                     |
|----|-------------------------------------------------------------------------------|-----------------------------------------------------------|
| 8  | [prefer-spock](prefer-spock/directive.md)                                     | Spock by default, even on Java                            |
| 9  | [prefer-spock-mocks](prefer-spock-mocks/directive.md)                         | Native Spock Mock/Stub in Spock suites                    |
| 10 | [prefer-mockito-under-junit](prefer-mockito-under-junit/directive.md)         | Mockito in JUnit suites                                   |
| 11 | [prefer-assertj-under-junit](prefer-assertj-under-junit/directive.md)         | AssertJ in JUnit suites                                   |
| 12 | [prefer-testcontainers-postgres](prefer-testcontainers-postgres/directive.md) | TestContainers with real PostgreSQL for persistence tests |

### Production code

Migrated from `coding-style.md`'s `production-code` ruleset (14 rules) plus `architecture-profile` and the
remaining pieces of `default-stack`. `error-handling`, `feature-structure` and `functional-style` were tagged
`stack: jvm` in the source; kept enabled by default here because the underlying rule does not name a specific
product, only a pattern — see each directive's own description for the caveat.

**Enabled**

| No | Id                                                              | Title                                               |
|----|-----------------------------------------------------------------|-----------------------------------------------------|
| 15 | [production-code](production-code/directive.md)                 | Production code assessment                          |
| 16 | [visibility](visibility/directive.md)                           | Lowest visibility by default                        |
| 17 | [naming](naming/directive.md)                                   | Domain-language names, verb-noun use cases          |
| 18 | [rich-domain](rich-domain/directive.md)                         | Behaviour lives on the domain object                |
| 19 | [error-handling](error-handling/directive.md)                   | Results over exceptions, no internal null           |
| 20 | [interfaces](interfaces/directive.md)                           | No interface without a reason                       |
| 21 | [abstraction-timing](abstraction-timing/directive.md)           | Stay concrete until the second use case             |
| 22 | [feature-structure](feature-structure/directive.md)             | Organise by feature, not by layer                   |
| 23 | [determinism](determinism/directive.md)                         | No ambient time or randomness in business logic     |
| 24 | [specifications](specifications/directive.md)                   | Explicit business rules as Specifications           |
| 25 | [single-responsibility](single-responsibility/directive.md)     | One responsibility per class                        |
| 26 | [framework-isolation](framework-isolation/directive.md)         | The domain drives the structure                     |
| 27 | [libraries-first](libraries-first/directive.md)                 | Check for an existing library before writing a util |
| 28 | [functional-style](functional-style/directive.md)               | Functional constructs where they clarify            |
| 29 | [no-explanatory-comments](no-explanatory-comments/directive.md) | Rename and extract instead of commenting            |
| 30 | [defer-discovered-gaps](defer-discovered-gaps/directive.md)     | Park a coverage gap, don't derail                   |
| 31 | [architecture-profile](architecture-profile/directive.md)       | Architecture the tool must respect                  |

**Disabled**

| No | Id                                                                          | Title                                                      |
|----|-----------------------------------------------------------------------------|------------------------------------------------------------|
| 32 | [prefer-lombok](prefer-lombok/directive.md)                                 | Prefer Lombok over hand-written boilerplate                |
| 33 | [prefer-liquibase-owned-schema](prefer-liquibase-owned-schema/directive.md) | Liquibase owns the schema, Hibernate never generates DDL   |
| 34 | [prefer-result-type-library](prefer-result-type-library/directive.md)       | Use the online.goodcode:result library for the Result type |

**Dropped from migration, flagged rather than silently lost:** `default-stack`'s Spring Boot preference was not
carried forward as a toggle — `choose-stack` (still to migrate, see protocol batches) now owns that decision
from task requirements, and a pre-loaded framework preference would work against `choose-stack`'s
"preferences only break ties" rule (plan decision 5). REST-Assured and the Java LTS pin were dropped as
separate toggles too, folded into no directive yet — say the word if either should get its own
`prefer-*` directive.

### Specs

Migrated from `spec-style.md` (batch 4 of 5) — rules for writing a spec file that `implement` can act on without
re-asking what "done" means.

**Enabled**

| No | Id                                                                    | Title                                                              |
|----|-----------------------------------------------------------------------|--------------------------------------------------------------------|
| 35 | [classify-task-shape](classify-task-shape/directive.md)               | Classify the shape of a candidate task                             |
| 36 | [one-task-granularity](one-task-granularity/directive.md)             | One spec is one thing a single implement run can finish            |
| 37 | [spec-rules](spec-rules/directive.md)                                 | How a spec is written                                              |
| 38 | [acceptance-criteria-format](acceptance-criteria-format/directive.md) | Acceptance criteria are the Given/When/Then rules, carried through |
| 39 | [definition-of-done](definition-of-done/directive.md)                 | What "done" means unless a spec says otherwise                     |
| 40 | [no-invented-requirements](no-invented-requirements/directive.md)     | Unknowns go to Open questions, never guessed                       |
| 41 | [dependencies-explicit](dependencies-explicit/directive.md)           | State ordering dependencies between specs                          |

**Disabled**

Empty — every migrated Specs directive is stack-agnostic, none needed `enabled-by-default: false`.

All migration batches complete (see the `craftsman` plan, "Kolejność realizacji", step 3). 41 directives total —
digest-style.md contributed none, it has no directive-kind entries.

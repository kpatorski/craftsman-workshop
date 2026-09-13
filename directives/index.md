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

## Directives

Grouped by category, one `##` section per topic. Each category has two tables: **Enabled** (what a protocol step
actually loads) and **Disabled** (installed, present, switched off). `craftsman list directives` reads both; a protocol
step loading directives for its `applies-when` reads only Enabled.

Rebuild into a two-level index (this file linking to `index-<category>.md`) once any single category passes ~200
entries — same restraint as `core.md`'s golden rule, applied to structure instead of fields.

### Testing

Migrated from `coding-style.md`'s test-writing sections. The agnostic ones (how a suite reads, how test data is
built) are enabled by default; the stack-specific ones (naming a concrete library) are disabled by default — see
`core.md`, "Fields specific to `directive`".

**Enabled**

| No | Id                                                    | Title                                          |
|----|--------------------------------------------------------|-------------------------------------------------|
| 1  | [test-style](test-style/directive.md)                 | How a test suite should read                   |
| 2  | [test-naming](test-naming/directive.md)               | Name a test by the state it describes          |
| 3  | [test-as-story](test-as-story/directive.md)           | Structure every test as given / when / then    |
| 4  | [suite-layout](suite-layout/directive.md)             | Tests on top, helpers at the bottom            |
| 5  | [test-data](test-data/directive.md)                   | Values and object building in tests            |
| 6  | [dummy-values](dummy-values/directive.md)             | Use placeholder values, not domain-specific ones |
| 7  | [test-fixtures](test-fixtures/directive.md)           | Extract a Fixture when object building repeats |

**Disabled**

| No | Id                                                                    | Title                                       |
|----|--------------------------------------------------------------------------|-----------------------------------------------|
| 8  | [prefer-spock](prefer-spock/directive.md)                               | Spock by default, even on Java                |
| 9  | [prefer-spock-mocks](prefer-spock-mocks/directive.md)                   | Native Spock Mock/Stub in Spock suites        |
| 10 | [prefer-mockito-under-junit](prefer-mockito-under-junit/directive.md)   | Mockito in JUnit suites                       |
| 11 | [prefer-assertj-under-junit](prefer-assertj-under-junit/directive.md)   | AssertJ in JUnit suites                       |
| 12 | [prefer-testcontainers-postgres](prefer-testcontainers-postgres/directive.md) | TestContainers with real PostgreSQL for persistence tests |
| 13 | [how-high-to-test](how-high-to-test/directive.md)                       | How high to test a behaviour                  |
| 14 | [stub-vs-in-memory](stub-vs-in-memory/directive.md)                     | Stub or in-memory implementation for a collaborator |

### Production code

Migrated from `coding-style.md`'s `production-code` ruleset (14 rules) plus `architecture-profile` and the
remaining pieces of `default-stack`. `error-handling`, `feature-structure` and `functional-style` were tagged
`stack: jvm` in the source; kept enabled by default here because the underlying rule does not name a specific
product, only a pattern — see each directive's own description for the caveat.

**Enabled**

| No | Id                                                                  | Title                                          |
|----|------------------------------------------------------------------------|---------------------------------------------------|
| 15 | [production-code](production-code/directive.md)                       | Production code assessment                        |
| 16 | [visibility](visibility/directive.md)                                 | Lowest visibility by default                      |
| 17 | [naming](naming/directive.md)                                         | Domain-language names, verb-noun use cases        |
| 18 | [rich-domain](rich-domain/directive.md)                               | Behaviour lives on the domain object               |
| 19 | [error-handling](error-handling/directive.md)                         | Results over exceptions, no internal null          |
| 20 | [interfaces](interfaces/directive.md)                                 | No interface without a reason                      |
| 21 | [abstraction-timing](abstraction-timing/directive.md)                 | Stay concrete until the second use case            |
| 22 | [feature-structure](feature-structure/directive.md)                   | Organise by feature, not by layer                  |
| 23 | [determinism](determinism/directive.md)                               | No ambient time or randomness in business logic    |
| 24 | [specifications](specifications/directive.md)                         | Explicit business rules as Specifications          |
| 25 | [single-responsibility](single-responsibility/directive.md)           | One responsibility per class                       |
| 26 | [framework-isolation](framework-isolation/directive.md)               | The domain drives the structure                    |
| 27 | [libraries-first](libraries-first/directive.md)                       | Check for an existing library before writing a util |
| 28 | [functional-style](functional-style/directive.md)                     | Functional constructs where they clarify           |
| 29 | [no-explanatory-comments](no-explanatory-comments/directive.md)       | Rename and extract instead of commenting           |
| 30 | [defer-discovered-gaps](defer-discovered-gaps/directive.md)           | Park a coverage gap, don't derail                  |
| 31 | [architecture-profile](architecture-profile/directive.md)             | Architecture the tool must respect                 |

**Disabled**

| No | Id                                                                        | Title                                          |
|----|--------------------------------------------------------------------------|-------------------------------------------------|
| 32 | [prefer-lombok](prefer-lombok/directive.md)                             | Prefer Lombok over hand-written boilerplate       |
| 33 | [prefer-liquibase-owned-schema](prefer-liquibase-owned-schema/directive.md) | Liquibase owns the schema, Hibernate never generates DDL |
| 34 | [prefer-result-type-library](prefer-result-type-library/directive.md)   | Use the online.goodcode:result library for the Result type |

**Dropped from migration, flagged rather than silently lost:** `default-stack`'s Spring Boot preference was not
carried forward as a toggle — `choose-stack` (still to migrate, see protocol batches) now owns that decision
from task requirements, and a pre-loaded framework preference would work against `choose-stack`'s
"preferences only break ties" rule (plan decision 5). REST-Assured and the Java LTS pin were dropped as
separate toggles too, folded into no directive yet — say the word if either should get its own
`prefer-*` directive.

Categories not yet migrated are filled in during the remaining migration batches from `coding-style.md` /
`spec-style.md` / `digest-style.md` (see the `craftsman` plan, "Kolejność realizacji", step 3).

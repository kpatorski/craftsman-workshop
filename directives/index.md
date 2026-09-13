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

Categories not yet migrated are filled in during the remaining migration batches from `coding-style.md` /
`spec-style.md` / `digest-style.md` (see the `craftsman` plan, "Kolejność realizacji", step 3).

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

## Protocols

Grouped by category, one `##` section per topic. Each category has two tables: **Enabled** (callable) and **Disabled**
(installed, present, switched off). `craftsman list protocols` reads both; dispatch to an `entry-point` reads only
Enabled.

Rebuild into a two-level index (this file linking to `index-<category>.md`) once any single category passes ~200
entries — same restraint as `core.md`'s golden rule, applied to structure instead of fields.

### Implementation

Migrated from `coding-style.md` / the `developer` skill (batch 3 of 5). `implement` is the entry point (see plan decision 7, formerly `/developer`); everything else is reached only through it or through a protocol it calls.

**Enabled**

| No | Id | Title | Note |
|----|----|-------|------|
| 1 | [implement](implement/protocol.md) | Drive a coding task in a HUMAN <-> AI loop | entry point |
| 2 | [scenario-new-use-case](scenario-new-use-case/protocol.md) | Add a new use case to an existing module |  |
| 3 | [scenario-change-existing-code](scenario-change-existing-code/protocol.md) | Change behaviour in existing code |  |
| 4 | [scenario-utils](scenario-utils/protocol.md) | Write or change a util |  |
| 5 | [scenario-missing-tests](scenario-missing-tests/protocol.md) | Cover existing code that lacks tests |  |
| 6 | [scenario-bootstrap-module](scenario-bootstrap-module/protocol.md) | Found a new project or module |  |
| 7 | [tdd-loop](tdd-loop/protocol.md) | Test-first implementation loop |  |
| 8 | [cover-cycle](cover-cycle/protocol.md) | Batch coverage cycle | repeats |
| 9 | [decide-test-level](decide-test-level/protocol.md) | Decide how high to test this |  |
| 10 | [scaffold-suite](scaffold-suite/protocol.md) | Create the empty test suite |  |
| 11 | [enumerate-test-cases](enumerate-test-cases/protocol.md) | List every known test case as a failing stub |  |
| 12 | [cover-batch](cover-batch/protocol.md) | Implement bodies for a small batch of stubs |  |
| 13 | [minimal-production-code](minimal-production-code/protocol.md) | Write the least production code that makes the batch pass |  |
| 14 | [review-design-direction](review-design-direction/protocol.md) | Confirm the design direction before the next batch |  |
| 15 | [snapshot-green](snapshot-green/protocol.md) | Snapshot the green suite before refactoring |  |
| 16 | [refactor-tests](refactor-tests/protocol.md) | Refactor the tests first |  |
| 17 | [refactor-production](refactor-production/protocol.md) | Refactor the production code |  |
| 18 | [finish-loop](finish-loop/protocol.md) | Close the loop |  |
| 19 | [characterize-loop](characterize-loop/protocol.md) | Characterization test loop |  |
| 20 | [characterize-cycle](characterize-cycle/protocol.md) | Characterization batch cycle | repeats |
| 21 | [enumerate-cases-from-code](enumerate-cases-from-code/protocol.md) | Read the code to list the cases it already handles |  |
| 22 | [characterize-batch](characterize-batch/protocol.md) | Lock in current behaviour for a small batch |  |
| 23 | [finish-characterize](finish-characterize/protocol.md) | Close the characterization loop |  |
| 24 | [commit-tests](commit-tests/protocol.md) | Commit the tests on their own |  |
| 25 | [bootstrap-module](bootstrap-module/protocol.md) | Module bootstrap |  |
| 26 | [choose-stack](choose-stack/protocol.md) | Agree the stack |  |
| 27 | [create-build](create-build/protocol.md) | Create the build |  |
| 28 | [add-dependencies](add-dependencies/protocol.md) | Add the agreed dependencies |  |
| 29 | [scaffold-package-skeleton](scaffold-package-skeleton/protocol.md) | Lay out the package skeleton |  |
| 30 | [base-configuration](base-configuration/protocol.md) | Add baseline configuration |  |
| 31 | [pick-first-aggregate](pick-first-aggregate/protocol.md) | Pick the first aggregate to implement |  |
| 32 | [locate-target](locate-target/protocol.md) | Locate the module / package / class to work in | shared |
| 33 | [create-empty-package](create-empty-package/protocol.md) | Create the empty target package |  |
| 34 | [challenge-the-util](challenge-the-util/protocol.md) | Confirm a util is really the right home |  |
| 35 | [read-existing-tests](read-existing-tests/protocol.md) | Read the existing suite first |  |
| 36 | [check-coverage](check-coverage/protocol.md) | Check the target is covered before changing it |  |
| 37 | [restate-current-behaviour](restate-current-behaviour/protocol.md) | Restate what the code currently does |  |
| 38 | [confirm-conventions](confirm-conventions/protocol.md) | Confirm structural conventions before creating classes | shared |

**Disabled**

Empty — nothing has been switched off yet. Populated by `craftsman disable protocol <id>`.

Categories not yet migrated are filled in during the remaining migration batches from `coding-style.md` / `spec-style.md` / `digest-style.md` (see the `craftsman` plan, "Kolejność realizacji", step 3).

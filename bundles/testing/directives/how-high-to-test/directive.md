---
id: how-high-to-test
title: How high to test a behaviour
description: >
  Picks the level a behaviour is tested at. Production code is package-private by default; something is public only when
  it is part of the cross-module communication API. Test as high as possible so tests read in business language and
  avoid needless mocking and duplication. Class-per-class testing is the thing being avoided, not a fallback.
applies-when: deciding what to write a test suite against, in `decide-test-level`
precedence: the project's existing test-level convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Default: one black-box suite per behaviour.

Levels:

- **one-black-box-suite** — default: behaviour reachable through a package / use-case entry point
- **dedicated-class-suite** — a class exists in its own right, not only to satisfy one collaborator
- **util-unit-suite** — the code is a shared util
- **split-suites-same-entry-point** — corner cases bloat one suite; several suites hit the same entry point, one concern
  each
- **extracted-strategy-suite** — the corner cases belong to a strategy that should be extracted, tested in full on its
  own, and stubbed in the main suite

Questions to ask when the level is unclear:

- Is there anything public in the module / package? → that public thing is a candidate for its own suite.
- Does class X exist only to satisfy class Y — remove Y, is X still needed? → X is a candidate for a
  dedicated-class-suite.
- Is it a util? → util-unit-suite.

Revisit when the suite is bloating with corner cases and losing readability during coverage or refactoring — propose
split-suites-same-entry-point or extracted-strategy-suite as a checkpoint.

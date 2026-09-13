---
id: testing
title: How a test suite is shaped
description: >
  The rules a test suite must satisfy regardless of methodology: how it reads, how test data is built, how deep to
  test a behaviour, and when a fake is a stub versus an in-memory implementation. Required by `tdd` and
  `legacy-code` — both drive a suite that must already look like this.
---

## Schema

No fields of its own — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Bundle

This is the suite-shape contract, independent of *how* the suite gets written. `tdd-loop` and `characterize-loop`
both produce a suite; both need it to read the same way, so this bundle is a dependency of both rather than owned
by either — the `tdd` and `legacy-code` bundles both `requires: [testing]` (batches 6 and 7 of this migration).

`test-style` composes `test-naming`, `test-as-story`, `suite-layout`; `test-data` composes `dummy-values`,
`test-fixtures` — both nest inside this bundle exactly as they did at the top level, `composes` is unaffected by
which folder an entry lives in.

## Directives

**Enabled**

| No | Id                                                             | Title                                                        |
|----|----------------------------------------------------------------|--------------------------------------------------------------|
| 1  | [test-style](directives/test-style/directive.md)               | How a test suite should read                                 |
| 2  | [test-naming](directives/test-naming/directive.md)             | Name a test by the state it describes                        |
| 3  | [test-as-story](directives/test-as-story/directive.md)         | Structure every test as given / when / then                  |
| 4  | [suite-layout](directives/suite-layout/directive.md)           | Tests on top, helpers at the bottom                          |
| 5  | [test-data](directives/test-data/directive.md)                 | Values and object building in tests                          |
| 6  | [dummy-values](directives/dummy-values/directive.md)           | Use placeholder values, not domain-specific ones             |
| 7  | [test-fixtures](directives/test-fixtures/directive.md)         | Extract a Fixture when object building repeats across suites |
| 8  | [how-high-to-test](directives/how-high-to-test/directive.md)   | How high to test a behaviour                                 |
| 9  | [stub-vs-in-memory](directives/stub-vs-in-memory/directive.md) | Stub or in-memory implementation for a collaborator          |

**Disabled**

Empty — nothing has been switched off yet.

## Protocols

None. This bundle is criteria only — the moments that apply them (`decide-test-level`, `scaffold-suite`...) live in
`tdd` and `legacy-code`, which both require this bundle.

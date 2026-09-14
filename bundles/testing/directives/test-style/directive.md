---
id: test-style
title: How a test suite should read
description: >
  A suite reads like a business analyst describing the system's requirements. It states behaviour, not mechanics — never which method was called or which argument was passed. Technical complexity hides behind small, human-named helpers.
applies-when: writing, extending or refactoring any test suite
composes: [test-naming, test-as-story, suite-layout]
precedence: the project's existing suite conventions win
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`. `composes` is the field a
composing directive uses to name the directives it assembles, one level or many.

## Directive

The test is the requirement document. A reader who does not know the code must be able to learn the business rules from
the suite alone, without reading the production code first. The three composed directives are how that is achieved:

1. [test-naming](../test-naming/directive.md) — the name states the resulting state, not a wish, not an implementation
   detail.
2. [test-as-story](../test-as-story/directive.md) — the body reads given / when / then.
3. [suite-layout](../suite-layout/directive.md) — tests on top, helpers at the bottom.

Enabling or disabling this directive enables or disables all three together; each can still be toggled on its own when
only part of the style is wanted.

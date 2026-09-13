---
id: test-data
title: Values and object building in tests
description: >
  Test data should lower the reader's cognitive load: placeholder values signal "irrelevant here", and object building is factored out once it repeats.
applies-when: building or stubbing an object inside a test
composes: [dummy-values, test-fixtures]
precedence: the project's existing test-data convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

1. [dummy-values](../dummy-values/directive.md) — placeholder values, not domain-specific ones.
2. [test-fixtures](../test-fixtures/directive.md) — extract a Fixture once object building repeats across suites.

Enabling or disabling this directive enables or disables both together; each can still be toggled on its own.

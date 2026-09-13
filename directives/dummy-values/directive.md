---
id: dummy-values
title: Use placeholder values, not domain-specific ones
description: >
  Stubbed and built objects use repeatable placeholders like "any-name", "any-street". The value signals it is irrelevant to the behaviour under test.
applies-when: choosing a value for a stubbed or built object in a test
precedence: the project's existing test-data convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Default: one repeatable placeholder per field — `any-<field>`.

Unless:

- the difference between two values matters for identity — use `any-name-a`, `any-name-b`
- the value carries business meaning (a zip-code that triggers a policy) — use the real business value
- two objects are compared — use natural-language markers pointing at the crux — `same-tenant` / `different-street`

When the same value set repeats within a suite, hide it inside a local factory method.

## Examples

    var userA = user("same-name", "same-zip-code", "any-street", "same-tenant");
    var userB = user("same-name", "same-zip-code", "different-street", "same-tenant");

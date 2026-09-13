---
id: error-handling
title: Results over exceptions, no internal null
description: >
  Business failures are modelled as data, not control flow. The pattern is language-agnostic; the concrete types below (Result, Optional) are JVM-flavored — swap for the equivalent in another language. Originally scoped `stack: jvm` in the source this was migrated from; kept as an ordinary directive here because the underlying rule does not name a specific product, only a pattern.
applies-when: a business operation can fail, or a value can be absent
precedence: the project's existing error-handling convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- business failures return `Result.failure(...)` — exceptions are not control flow
- never pass null internally; model absence with `Optional` / `Result` / `Either`
- if you must throw, throw a named domain `RuntimeException`, never a raw or checked one

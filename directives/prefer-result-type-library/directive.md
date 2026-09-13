---
id: prefer-result-type-library
title: Use the online.goodcode:result library for the Result type
description: >
  The JVM implementation for [error-handling](../error-handling/directive.md)'s Result pattern — a concrete library choice, not the pattern itself. Split out from the old `default-stack` reference so it can be toggled independently of the rest of the JVM stack.
applies-when: a JVM project needs a concrete Result type to satisfy error-handling
precedence: the project's existing Result / Either implementation wins
enabled-by-default: false
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). `enabled-by-default: false`
because this names a concrete library — see core.md, "Fields specific to `directive`".

## Directive

Must:

- use `online.goodcode:result` for `Result.success(...)` / `Result.failure(...)`, rather than a hand-rolled Result type
  or a different library
- if the target module does not already depend on it, ask before adding the dependency

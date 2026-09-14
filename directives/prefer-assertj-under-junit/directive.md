---
id: prefer-assertj-under-junit
title: AssertJ in JUnit suites
description: >
  A JUnit suite asserts with AssertJ's fluent `assertThat(...)`, not JUnit's own assertion methods. Spock suites do not need this — Spock's native condition blocks already read fluently.
applies-when: asserting in a JUnit suite
precedence: the project's existing assertion library wins
enabled-by-default: false
---

## Schema

Introduces no new fields — see `core.md`. `enabled-by-default: false`
because this names a concrete library — see `core.md`, "Fields specific to `directive`".

## Directive

Must:

- JUnit suites assert with AssertJ — `assertThat(...)`
- Spock suites use Spock's native condition blocks, not an assertion library

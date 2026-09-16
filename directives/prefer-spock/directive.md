---
id: prefer-spock
title: Spock by default, even on Java
description: >
  Spock is chosen for readability — native given/when/then, data tables, expressive assertions. A stack-specific
  preference: only relevant once the stack itself includes the JVM, and only breaks a tie between test frameworks — it
  never pre-decides the stack. See `choose-stack`.
applies-when: choosing or writing a test suite on a JVM project
precedence: the project's existing test framework wins
enabled-by-default: false
---

## Schema

Introduces no new fields — see `core.md`. `enabled-by-default: false`
because this names a concrete library, not an agnostic rule — see `core.md`, "Fields specific to `directive`".

## Directive

Default: Spock, latest stable major.

Falls back to JUnit when the project already standardises on JUnit, or Groovy is unavailable in the build.

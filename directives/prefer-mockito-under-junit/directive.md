---
id: prefer-mockito-under-junit
title: Mockito in JUnit suites
description: >
  A JUnit suite mocks and stubs with Mockito, not a competing library. Split out from the old `mocking-tooling` rule's JUnit side so it can be toggled independently of the Spock side — see `prefer-spock-mocks`.
applies-when: a JUnit suite needs a mock or a stub for a collaborator
precedence: the project's existing mocking convention wins
enabled-by-default: false
---

## Schema

Introduces no new fields — see `core.md`. `enabled-by-default: false`
because this names a concrete library — see `core.md`, "Fields specific to `directive`".

## Directive

Must:

- JUnit suites use Mockito
- never mix mocking libraries within a suite

Companion directive for Spock suites: [prefer-spock-mocks](../prefer-spock-mocks/directive.md).

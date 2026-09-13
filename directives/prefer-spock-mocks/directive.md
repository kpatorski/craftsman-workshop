---
id: prefer-spock-mocks
title: Native Spock Mock/Stub in Spock suites
description: >
  A Spock suite mocks and stubs with Spock's own `Mock()` / `Stub()`, not a separate mocking library. Whether to mock at all is governed by the `stub-vs-in-memory` heuristic and the black-box testing rules — this directive is only about which library, once mocking is the right call.
applies-when: a Spock suite needs a mock or a stub for a collaborator
precedence: the project's existing mocking convention wins
enabled-by-default: false
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). `enabled-by-default: false` because this names a concrete library — see core.md, "Fields specific to `directive`".

## Directive

Must:

- Spock suites use Spock's own `Mock()` / `Stub()`
- never mix mocking libraries within a suite

Companion directive for JUnit suites: [prefer-mockito-under-junit](../prefer-mockito-under-junit/directive.md).

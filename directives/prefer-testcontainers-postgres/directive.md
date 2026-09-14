---
id: prefer-testcontainers-postgres
title: TestContainers with real PostgreSQL for persistence tests
description: >
  Persistence-touching tests run against a real PostgreSQL in TestContainers, not an in-memory or mocked database. JUnit Jupiter is used only to bootstrap the container, even inside a Spock suite. Split out from the old `default-stack` reference so it can be toggled independently of the rest of the JVM stack.
applies-when: a test needs a real database rather than a stub or in-memory fake — see the `stub-vs-in-memory` heuristic
precedence: the project's existing test infrastructure wins
enabled-by-default: false
---

## Schema

Introduces no new fields — see `core.md`. `enabled-by-default: false`
because this names concrete infrastructure — see `core.md`, "Fields specific to `directive`".

## Directive

Must:

- persistence tests run against PostgreSQL in TestContainers, not H2 or a mock
- JUnit Jupiter bootstraps the container even when the suite itself is Spock

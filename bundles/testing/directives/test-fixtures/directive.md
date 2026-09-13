---
id: test-fixtures
title: Extract a Fixture when object building repeats across suites
description: >
  Same principle as extracting a helper method, but across suites. A package-level class (e.g. UserFixture) exposes intent-named builders and stubbers for complex objects.
applies-when: the same complex build or stub appears in more than one suite
precedence: the project's existing test-data convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- fixture methods are domain-named (`aValidReservation`, `aReservationWithExpiredDeadline`)
- fixtures stay readable, free of unnecessary technical detail

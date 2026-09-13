---
id: scenario-change-existing-code
title: Change behaviour in existing code
description: >
  The kind of change is known (business requirements in hand). Very close to scenario-new-use-case, but the suite and production code already exist — the loop adds to them rather than creating from scratch.
input: existing code, its test suite, and the new business rules the change must satisfy
output: same as tdd-loop's output — the existing suite and production code extended, green and refactored
match: task is to modify or extend the behaviour of code that already exists and has tests
steps: [locate-target, read-existing-tests, check-coverage, restate-current-behaviour, confirm-conventions, tdd-loop]
overrides:
  enumerate-test-cases: means adding stubs or assertions to the existing suite, following its convention, not starting a new one
  decide-test-level: skip — the existing suite already fixes the level; only run it if the change shifts the level
done-when: tdd-loop's done-when holds
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). `overrides` is defined there,
"Fields specific to `protocol`".

## Protocol

1. [locate-target](../locate-target/protocol.md) — find the existing class and its suite.
2. [read-existing-tests](../read-existing-tests/protocol.md) — learn current behaviour and conventions.
3. [check-coverage](../check-coverage/protocol.md) — confirm the target is covered before changing it.
4. [restate-current-behaviour](../restate-current-behaviour/protocol.md) — state the baseline in plain language.
5. [confirm-conventions](../confirm-conventions/protocol.md) — settle any placement decision the change forces.
6. [tdd-loop](../../bundles/tdd/protocols/tdd-loop/protocol.md) — extend the suite and the production code, with the overrides above applied to
   its `enumerate-test-cases` and `decide-test-level` steps.

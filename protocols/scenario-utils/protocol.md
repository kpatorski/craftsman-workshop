---
id: scenario-utils
title: Write or change a util
description: >
  Utils are avoided, but occasionally genuinely needed. A util is shared code, so it is tested at unit level — the class
  itself — never through a module entry point. This is the one place where a test name may reference the util method.
input: a genuine need for stateless, shared code with no domain identity
output: same as tdd-loop's output — a green, refactored suite and production code for the util
match: task is to add or change a genuine utility — stateless, shared, no domain identity
steps: [challenge-the-util, locate-target, tdd-loop]
overrides:
  decide-test-level: forced to util-unit-suite — skip the how-high-to-test question
  test-naming: the method-name exception applies — a test may name the util method when clearer
done-when: tdd-loop's done-when holds
---

## Schema

Introduces no new fields — see `core.md`. `overrides` is defined there,
"Fields specific to `protocol`".

## Protocol

1. [challenge-the-util](../challenge-the-util/protocol.md) — confirm a util is really the right home.
2. [locate-target](../locate-target/protocol.md) — find where the util belongs.
3. [tdd-loop](../../bundles/tdd/protocols/tdd-loop/protocol.md) — build it test-first, with the overrides above applied
   to its `decide-test-level` step and to the [test-naming](../../bundles/testing/directives/test-naming/directive.md)
   directive.

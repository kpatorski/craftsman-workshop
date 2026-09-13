---
id: scenario-missing-tests
title: Cover existing code that lacks tests
description: >
  A gap in coverage on code that already works. Runs on its own; the tests land in a separate commit. If the current behaviour looks wrong, the gap is noted, not fixed here.
input: existing, working code with no tests covering it
output: same as characterize-loop's output — passing characterization tests, committed on their own
match: task is to add tests for existing, working behaviour that is currently uncovered
steps: [characterize-loop]
done-when: characterize-loop's done-when holds
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. [characterize-loop](../characterize-loop/protocol.md) — lock in current behaviour with passing tests, no production
   code changes.

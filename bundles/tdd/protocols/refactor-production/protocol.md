---
id: refactor-production
title: Refactor the production code
description: >
  Refactors the production code, once the suite is in good shape.
input: the refactored, green suite from refactor-tests
output: refactored production code; whole suite green
uses: [production-code]
checkpoint:
  type: ask
  blocking: true
  shows: [production-diff]
  prompt: "Production code after refactor — diff, suite green. Close the loop?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Apply the [production-code](../../../../directives/production-code/directive.md) directive.
2. Re-run the full relevant suite after each change.
3. Stop and fix immediately on any red.

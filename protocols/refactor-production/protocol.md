---
id: refactor-production
title: Refactor the production code
description: >
  Only once the suite is in good shape. Apply the production-code directive, re-running the full relevant suite after each change. Stop and fix immediately on any red.
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

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [tdd-loop](../tdd-loop/protocol.md).

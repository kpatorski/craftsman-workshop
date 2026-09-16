---
id: stub-vs-in-memory
title: Stub or in-memory implementation for a collaborator
description: >
  Pick whichever reads better in the suite. The deciding factor is the number and complexity of the interface methods
  you would have to stub or implement — few simple methods lean stub; many methods, or interdependent state across
  calls, lean in-memory.
applies-when: a test needs a fake for a collaborator instead of a mock
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

No fixed default — decided per case on readability.

- Lean stub when the interface has few, simple methods used in isolation.
- Lean in-memory when the interface has many methods, or the test needs consistent state across several calls.

---
id: functional-style
title: Functional constructs where they clarify
description: >
  Functional constructs replace null checks and manual loops when they read better — clarity is the test, not novelty. The named types (Optional, Stream) are JVM-flavored; the underlying idea generalizes to any language with the equivalent constructs.
applies-when: a null check or a manual loop could be replaced with a functional construct
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- prefer Optional / Stream / Either / Result over null checks and manual loops when it improves clarity
- use modern language and library APIs (e.g. `"x".formatted(y)`) when they read better — not for novelty

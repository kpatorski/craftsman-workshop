---
id: interfaces
title: No interface without a reason
description: >
  An interface is justified by a second real implementation, or an explicit strategic reason such as a port or a testing
  seam at a boundary — never introduced "just in case".
applies-when: deciding whether to introduce an interface
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- an interface needs a second real implementation or an explicit strategic reason (port, testing seam for a boundary)
- never a `SomethingServiceImpl` — name the concrete class after what it does

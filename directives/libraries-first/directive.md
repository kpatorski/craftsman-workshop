---
id: libraries-first
title: Check for an existing library before writing a util
description: >
  A project-local utility is a last resort, checked against the standard library, the framework already in use, and well-known utility libraries first.
applies-when: about to write a utility method
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- before creating a utility method, check Apache Commons, Vavr, the standard library, and the framework already in use
- do not create project-local utilities prematurely

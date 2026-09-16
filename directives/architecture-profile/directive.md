---
id: architecture-profile
title: Architecture the tool must respect
description: >
  Applied when a protocol decides where a class lives and how modules talk. Anything already fixed by the existing
  project or a project-level style wins over this profile.
applies-when: deciding where a class or module lives, or how two modules communicate
precedence: the project's existing architecture wins — this is a default, not a mandate
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Style: Clean Architecture — default, overridable per project. Also respected: DDD tactical patterns, bounded-context
isolation, application logic kept out of infrastructure.

Layering:

- domain has no dependency on framework, persistence or transport
- use case orchestrates domain; depends inward only
- adapters (entrypoint, db) depend on the use case, never the reverse

Communication: events between bounded contexts; ports & adapters at the boundary.

Package layout: see [feature-structure](../feature-structure/directive.md).

Assumes event storming is done — events, aggregates, commands and views are known before implementation starts. See the
`domain-design` entry point for how that gets produced.

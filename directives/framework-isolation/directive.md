---
id: framework-isolation
title: The domain drives the structure
description: >
  The domain's shape comes from the domain, never from annotations, DTOs, persistence or transport objects. Framework code adapts around the domain, not the other way round.
applies-when: a framework concern (an ORM, a serialization library, a web layer) meets a domain class
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- the domain shape is not dictated by annotations, DTOs, persistence or transport objects
- framework code adapts around the domain, not the other way round

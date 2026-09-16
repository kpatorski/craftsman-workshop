---
id: rich-domain
title: Behaviour lives on the domain object
description: >
  Business rules sit on the domain object or the use-case boundary, never in a data-free service that only shuffles
  other objects around.
applies-when: deciding where a business rule or behaviour belongs
precedence: the project's existing domain modelling convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- business rules sit on the domain object or the use-case boundary, not in a data-free service
- domain business methods return a Result or an event — never void, never throws for business outcomes

Avoid: anemic data-only domain objects.

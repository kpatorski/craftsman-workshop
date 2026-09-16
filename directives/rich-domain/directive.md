---
id: rich-domain
title: Behaviour lives on the domain object
description: >
  Business rules sit on the domain object; on a domain service or a factory when no single object can honestly
  own them; or at the use-case boundary. Never in a data-free service that only shuffles other objects around.
applies-when: deciding where a business rule, a behaviour, or construction logic belongs
precedence: the project's existing domain modelling convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Four legitimate homes for behaviour — pick the first one that honestly fits, in order:

1. **The domain object** — default. An entity or a value object (see `value-objects`). Its business methods
   return a Result or an event — never void, never throws for business outcomes.
2. **A domain service** — only when the behaviour genuinely involves more than one aggregate, or belongs to the
   domain but to no single object (a transfer between two accounts; a policy needing several aggregates' state).
   All of these must hold, or it is not a domain service:
   - stateless
   - named in ubiquitous language after what it does in the domain — see `naming`. A `...Service` that is really a
     use case is a use case, not a domain service.
   - takes domain objects in, returns domain objects or a Result out — never a repository, a framework type or a
     transport type
   - lives in the domain layer (see `architecture-profile`) and needs no interface unless a second real
     implementation exists — see `interfaces`
3. **A factory** — when creating a valid instance is itself non-trivial: the invariant must hold at birth, several
   objects must be created together consistently, or reconstitution differs from creation. A factory is a named
   domain concept (a static creator on the aggregate root, or its own small class) — not a `...Factory` util.
   Creation that is one constructor call does not get a factory — see `abstraction-timing`.
4. **The use-case boundary** — orchestration, IO, transaction, calling a port. Not business decisions.

Avoid: anemic data-only domain objects. The reason a data-free service is wrong is that the logic had an owner and
was moved off it — a domain service is correct only when the logic genuinely has no single owner. If the
"service" operates on one aggregate's data, it is that aggregate's method.

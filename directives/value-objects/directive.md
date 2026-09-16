---
id: value-objects
title: Concepts without identity are Value Objects
description: >
  A concept the application only cares about the value of — not which instance it is — is an immutable Value
  Object: equality by attributes, no id, validated at construction. Covers the entity-vs-value call and the
  primitive standing in for a domain concept.
applies-when: modelling a domain concept as a class, or a primitive is standing in for a domain concept
precedence: the project's existing domain modelling convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

The deciding question: does the application need to tell two instances with identical attributes apart, and
follow one of them through time? Yes → entity, it gets an id. No → value object. **Value object is the default;
an entity is the exception that has to justify its id.**

Must:

- immutable — no setter, no mutating method; a "change" returns a new instance
- equality and hash by attributes, never by reference or id
- valid at construction or not constructed — a `Money` cannot exist with a negative amount and no currency. Where
  invalidity is a business outcome rather than a programmer error, construction returns a `Result` — see
  `error-handling`.
- behaviour lives on the value object too (`Money.add`, `DateRange.overlaps`), side-effect-free, returning new
  values. This is not an exception to `rich-domain` — it is `rich-domain`'s "the domain object", including value
  objects.
- a primitive standing in for a domain concept is a missing value object — `String email`, `BigDecimal price`, two
  loose `LocalDate`s are `EmailAddress`, `Money`, `DateRange` waiting to be named. See `naming` for the vocabulary
  that names them.
- no repository, no independent persistence — stored as part of whichever entity or aggregate holds it
- an ORM demanding a no-arg constructor or mutable fields does not get to reshape the value object — see
  `framework-isolation`

A value object *carries* a value; a rule *about* values that is worth naming and composing is a
`specifications`-pattern Specification, not a value object.

## Examples

- `DeskId` — a value object wrapping the identity of a different aggregate.
- `Money`, `BookingPeriod` — immutable, validated, with their own behaviour.
- Counter-example: `Reservation` is an entity, not a value object — two reservations with identical desk, day and
  employee are still two distinct reservations if made twice by mistake, and the system needs to tell them apart
  to cancel the right one.

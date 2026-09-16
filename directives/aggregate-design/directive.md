---
id: aggregate-design
title: Small aggregates, referenced by identity
description: >
  An aggregate is only as large as the invariant it protects; everything outside that boundary is referenced by
  id, never by object reference. Sizing and reference rules only — which events group under which aggregate is
  decided while modelling, in `identify-aggregates`, not here.
applies-when: drawing an aggregate boundary, or a domain class needs to refer to another aggregate
precedence: the project's existing domain modelling convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- the boundary is the invariant, nothing more — whatever must be true at the end of every single transaction
  defines the aggregate; anything that may be briefly stale belongs outside it. A field that is only ever read,
  never used to decide, is not a reason to pull another entity inside the boundary.
- reference other aggregates by identity only — a domain class holds `DeskId`, never a `Desk`. Three concrete
  consequences, because the rule is useless without them: no lazily navigating to the other aggregate and mutating
  it; the use case, not the domain class, loads a second aggregate if it genuinely needs one; the object graph you
  load stops at the boundary, so "one aggregate" is also one unit of loading and locking.
- a collection inside an aggregate has a bounded, known size — a one-to-many that grows with usage (every
  reservation ever made against a cycle) is the signature of a too-large aggregate. Name the id-referenced child
  aggregate instead and query it.
- changes across aggregates are eventually consistent, and the mechanism is named — one transaction modifies one
  aggregate. Another aggregate that must react does so via a subscriber to the first one's event, a process
  manager, or a reconciling job — say which, and say what lag is acceptable. "It just stays in sync" is the same
  failure as claiming an aggregate protects something it structurally cannot see.

Legitimate exception, stated so it can't be abused: two entities stay in one aggregate when a true invariant spans
them *and* the resulting object is still small and bounded. "It's more convenient to load them together" is not
that.

Which events fall inside a boundary is `identify-aggregates`' call while modelling; how many classes sit over the
resulting persisted record is `feature-structure`'s. This directive only sizes the boundary and types the
reference between two already-decided aggregates.

## Examples

- `Reservation` holds `DeskId` and `EmployeeId`, never `Desk` and `Employee`.
- `BookingCycle` started as "a cycle with its reservations" — once a cycle can hold thousands, it becomes "a
  cycle" plus id-referenced `Reservation`s, not a cycle whose collection keeps growing.
- Counter-example where merging is right: `Desk` protecting "no double booking for a day" needs every reservation
  for that desk in the same transaction — that invariant cannot be eventually consistent, so it stays inside one
  boundary (see `identify-aggregates`' own merge resolution).

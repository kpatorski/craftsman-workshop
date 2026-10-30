---
id: module-dependencies
title: Dependencies point one way and go through the front door
description: >
  Modules and classes depend on each other in one direction, with no cycles, and only through what the other side
  publishes. A model that is not this context's own — another context's, a legacy system's, an external service's —
  is translated at the boundary and never spreads into this context's code.
applies-when: >
  adding or changing a dependency between modules, packages or classes, or code that talks to another bounded
  context, a legacy system or an external service
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- dependencies between modules and between packages point one way; no cycle, however long — `A → B → C → A` is as
  much a cycle as `A → B → A`
- a module uses another only through what that module publishes — its API, its commands, its events; never its
  internal packages, its repositories, its entities or its tables
- every table has one owning module; another module that needs the data asks the owner, or keeps its own copy fed by
  the owner's events
- a model this context does not own is translated at the boundary by an anti-corruption layer: an adapter that turns
  the other side's types into this context's own, and back. The domain and the use cases never see the other side's
  classes — its DTOs, its generated client, its enums
- an anti-corruption layer is required when the other side is a legacy system, an external service, or a context whose
  model this team does not control; between two contexts the same team owns, a published API or event is enough
- a class gets what it depends on from outside — through its constructor — and never fetches it itself: no static
  access to infrastructure, no `new` of a repository or a client inside domain or use case code
- a class talks to what it holds, not to what that returns: `reservation.cancel()`, never
  `reservation.getDesk().getFloor().release(...)`
- a new dependency between modules is declared where the build declares module dependencies, never left to whatever
  happens to be on the classpath

Must not:

- break a cycle by moving the shared part into a `common` or `shared` module that every module then depends on —
  the shared part belongs to the module that owns its meaning, or is duplicated where each side needs a different
  view of it
- pass another context's type through this context's API, even unchanged

How contexts relate and which side translates is decided with the domain model (the `draw-bounded-contexts`
protocol); this directive checks that the code keeps to it. Which way layers depend is
[architecture-profile](../architecture-profile/directive.md)'s; how a class's size and responsibilities show in its
dependencies is [single-responsibility](../single-responsibility/directive.md)'s.

## Examples

`booking` imports `billing.internal.InvoiceRepository` to read whether a reservation is paid → the import crosses into
`billing`'s internals; `billing` publishes `isPaid(ReservationId)` or a `ReservationPaid` event, and `booking` uses
that.

`booking` calls a legacy HR system whose client returns `EmpRecordDTO` with a `deptCd` field. An adapter in `booking`
turns it into `Employee` with a `Department`; no class outside that adapter imports `EmpRecordDTO`.

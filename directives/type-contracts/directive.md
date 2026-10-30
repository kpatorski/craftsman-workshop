---
id: type-contracts
title: A subtype keeps its parent's promise, an interface asks only what its client uses
description: >
  A class that implements an interface or extends a class does everything that type promises, so a caller never has
  to know which one it holds. Code is reused by composition, not by inheritance. An interface is as narrow as the
  client that uses it. A new variant is a new type, not another branch in every place that checks the variants.
applies-when: >
  writing or changing an interface, an implementation of one, a subclass, an override, or code that branches on the
  kind of an object
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- an implementation or an override keeps the promise of the type it implements: it accepts every input the type
  accepts, gives what the type says it gives, and fails only the ways the type says it may fail
- behaviour is reused by composition: a class that needs what another does holds it and calls it. A class extends
  another only when it truly is that type and keeps all of its promise — never to borrow its code
- a caller works with the type it was given; it never checks which implementation it holds to decide what to do
- an interface holds what one kind of client uses; a client that needs one method of a broad interface gets a
  narrower one, owned by the client — a port per use case
- when the variants of something differ in behaviour, each variant is its own type and carries its own behaviour; a
  new variant is a new type, not a new branch added to every `switch` over the variants. One exhaustive `switch` over
  a sealed type, where the compiler names a missing variant, is fine

Must not:

- an override that throws `UnsupportedOperationException`, does nothing, or ignores an argument the type promises to
  use — it is a sign the class is not really that type
- `instanceof` or a type field checked by a caller to choose behaviour that belongs on the type
- an abstract base class whose purpose is to share code between its subclasses — the shared code goes into a class
  the former subclasses hold
- an extension point for a variant that does not exist yet — see
  [abstraction-timing](../abstraction-timing/directive.md)

One responsibility per class is [single-responsibility](../single-responsibility/directive.md)'s; the domain depending
on ports rather than on infrastructure is [architecture-profile](../architecture-profile/directive.md)'s and
[module-dependencies](../module-dependencies/directive.md)'s.

## Examples

`ReadOnlyReservationRepository implements ReservationRepository` whose `save` throws `UnsupportedOperationException`
→ it is not a `ReservationRepository`; the read-only use case gets a port with only the reads it needs.

`AbstractNotifier` with `send()` and `retry()`, extended by `MailNotifier` and `SmsNotifier` only to reuse `retry()`
→ a `Retry` class both hold, and two notifiers that implement `Notifier`.

`if (payment instanceof CardPayment) {...} else if (payment instanceof BankTransfer) {...}` in three use cases →
`payment.settle(...)` on each payment type; adding `Blik` adds one type, not a branch in three places.

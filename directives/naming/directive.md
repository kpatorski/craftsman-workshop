---
id: naming
title: Domain-language names, verb-noun use cases
description: >
  Production code names come from the domain's ubiquitous language, not from technical roles. A name is complete
  enough that the signature alone, with the body collapsed, says what the code does.
applies-when: naming a class, method, parameter, field or use case in production code
precedence: the project's existing naming convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- use cases are verb-noun (`CreateReservation`, `CloseVoting`)
- names follow the domain's ubiquitous language
- the collapsed-body test passes: with the body hidden, a method's name, its parameters and its return type say what
  it does and what it gives back; a class's name and its public methods say what it is for. Needing to open the body
  to know that means the name, or a type in the signature, is wrong
- names are whole words: `reservation`, not `res`; `customerAddress`, not `custAddr`. An abbreviation stays only when
  it is the word the domain itself uses (`IBAN`, `VAT`) or one every developer reads as a word (`id`, `url`)

Forbidden in a name: `Service`, `Impl`, `Manager`, `Helper`, `Handler`, `Resolver`, `Processor` — each names a
technical role, not what the class does. The words a test's name must not use belong to the `test-naming` directive.

`Utils` is the exception to the exceptions: a stateless class of functions over a type the project does not own
(`DateTimeUtils` over `java.time`), with nothing of the domain in it, and only when no library already in use
provides them — see [libraries-first](../libraries-first/directive.md). Anything that speaks the domain's language is
not a util; it is named for what it does.

## Examples

`ReservationService.process(String id, boolean flag)` — the collapsed body tells nothing: `CancelReservation.cancel(
ReservationId reservation, CancellationReason reason)` does.

`calcTotAmt(List<Item> itms)` → `totalPrice(List<OrderLine> lines)`.

`EmailHelper` → `ReservationConfirmationMail`, named for what it sends.

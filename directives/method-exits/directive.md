---
id: method-exits
title: A method's condition says when it does its work
description: >
  A method that returns nothing and works only under some condition states that condition once, as the reason to do
  its work — never as a row of bare `return;` exits taken before it, the way a `goto` jumps out.
applies-when: writing or changing a method that returns nothing and does its work only when some condition holds
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- the condition says when the method does its work: `if (a && !b) { work(); }`, never `if (!a) return; if (b) return;
  work();`
- several conditions are one predicate named in the domain's language — `if (order.isReadyToSend())` — on the object
  that holds the data it reads, or a private method of the class when no such object exists
- the predicate is named for what must hold for the work to happen, not for what stops it

Must not:

- a bare `return;` that leaves a method returning nothing before its work, whether at the top or in the middle
- invert a condition only to make room for an early exit

A condition the caller must learn about — the work is refused for a business reason — is not a silent exit at all: it
is a result or an error the caller receives, see [error-handling](../error-handling/directive.md). A method that
returns a value returns it where it is computed; this directive is about methods that return nothing.

## Examples

Before — three exits before the work:

```java
void sendReminder(Reservation reservation) {
    if (reservation.isCancelled()) return;
    if (reservation.reminderSent()) return;
    if (!reservation.startsWithin(Duration.ofHours(24))) return;
    mailer.send(reminderFor(reservation));
}
```

After — one condition, named for when the work happens:

```java
void sendReminder(Reservation reservation) {
    if (reservation.isDueForReminder(clock)) {
        mailer.send(reminderFor(reservation));
    }
}
```

`isDueForReminder` lives on `Reservation`, because the three facts it combines are the reservation's own.

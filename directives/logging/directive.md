---
id: logging
title: Log what someone will need to find, once, without secrets
description: >
  A log is read by someone looking for what happened to one thing at one moment. What matters is logged once, where it
  is decided, at a level that says how urgent it is, with the ids that find it — and never with data that must not
  leave the system.
applies-when: >
  writing or changing code that logs, or code that decides a business outcome, handles a failure, or calls another
  system
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- a decision that matters to whoever runs the system is logged where it is made: a business operation done or
  refused, a state that changed, a call to another system that failed — with what happened, to which thing, and why
- the thing is named by its id (`reservationId=42`), never by printing the whole object
- the level says who needs to act: `ERROR` — someone must act now; `WARN` — handled, but worth a look; `INFO` — a
  business event or a change of state; `DEBUG` — detail for diagnosing, off in production
- the message is a fixed text with the values passed as parameters, so it can be searched for and costs nothing when
  the level is off: `log.info("Reservation cancelled, reservationId={}", id)`
- a failure is logged once, where it is handled, with the exception itself passed to the logger so the stack trace
  stays — not only its message
- logging lives at the edges — the use case and the adapters; a domain object returns its result or its event, and
  the use case logs it

Must not:

- personal data, passwords, tokens, keys, session ids, payment data, or whole request and response bodies — leave
  them out, or mask them, in every message and every parameter
- log and rethrow: the same failure then appears once per layer it passes
- build the message by concatenating strings
- log at `INFO` inside a loop over items, where one summary line says the same

## Examples

Before — logged at every layer, with the whole object, and the stack trace lost:

```java
catch (PaymentFailed e) {
    log.error("Error: " + e.getMessage() + " for " + reservation);
    throw e;
}
```

After — logged once, in the use case that handles the failure:

```java
catch (PaymentFailed e) {
    log.warn("Reservation not paid, will retry, reservationId={}", reservation.id(), e);
    return retryLater(reservation);
}
```

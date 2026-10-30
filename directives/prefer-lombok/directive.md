---
id: prefer-lombok
title: Prefer Lombok over hand-written boilerplate
description: >
  On JVM projects, every constructor, accessor and builder Lombok can generate is generated, never written by hand.
  Accessors are fluent, like a record's — `name()`, never `getName()` — and a setter, where one is needed, returns
  the object so calls chain.
applies-when: writing or changing a JVM class that has or needs a constructor, an accessor, a setter or a builder
precedence: the project's existing convention wins — if the codebase hand-writes boilerplate, follow the codebase
enabled-by-default: false
---

## Schema

Introduces no new fields — see `core.md`. `enabled-by-default: false` because this names a concrete library — see
`core.md`, "Fields specific to `directive`".

## Directive

- Whatever Lombok can generate is not written by hand: a constructor, an accessor, a setter, a builder, `equals`,
  `hashCode`, `toString`. A hand-written one is kept only when it does something the generated one cannot.
- `@RequiredArgsConstructor` / `@AllArgsConstructor` / `@NoArgsConstructor` instead of a hand-written constructor —
  including one that exists only to be private or empty: `@NoArgsConstructor(access = AccessLevel.PRIVATE)`, not
  `private Foo() {}`.
- `@Accessors(fluent = true, chain = true)` — an accessor is `name()`, not `getName()`, the way a record's is; a
  setter is `name(value)`, not `setName(value)`, and returns the object: `reservation.status(CANCELLED).note(reason)`.
- A setter exists only where the field must change after construction; an immutable class has none.
- `@Builder` only when a constructor has more than three parameters, or optional ones.
- Never `@Data` — it pulls in `equals`, `hashCode` and `toString` unasked. Pick the annotations you need.
- If the target module does not already depend on Lombok, ask before adding the dependency.

## Examples

Instead of a 12-line constructor plus getters, the class is:

    @RequiredArgsConstructor
    @Accessors(fluent = true)
    @Getter
    class Reservation {
        private final DeskId desk;
        private final Period period;
    }

A class whose status changes after construction:

    @Accessors(fluent = true, chain = true)
    @Getter
    class Ticket {
        private final TicketId id;
        @Setter private Status status;
        @Setter private String note;
    }

    ticket.status(CLOSED).note("duplicate of T-12");

---
id: prefer-lombok
title: Prefer Lombok over hand-written boilerplate
description: >
  On JVM projects, generate constructors, accessors and builders with Lombok annotations instead of writing them by hand. Accessors are fluent — `name()`, never `getName()`. Split out from the old `default-stack` reference so it can be toggled independently of the rest of the JVM stack.
applies-when: writing or changing a JVM class that needs a constructor, an accessor or a builder
precedence: the project's existing convention wins — if the codebase hand-writes boilerplate, follow the codebase
enabled-by-default: false
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). `enabled-by-default: false`
because this names a concrete library — see core.md, "Fields specific to `directive`".

## Directive

- `@RequiredArgsConstructor` / `@AllArgsConstructor` instead of a hand-written constructor.
- `@Accessors(fluent = true)` — an accessor is `name()`, not `getName()`.
- `@Builder` only when a constructor has more than three parameters, or optional ones.
- Never `@Data` — it pulls in `equals`, `hashCode` and `toString` unasked. Pick the annotations you need.
- If the target module does not already depend on Lombok, ask before adding the dependency.

## Examples

Instead of a 12-line constructor plus getters, the class is:

    @RequiredArgsConstructor
    @Accessors(fluent = true)
    class Reservation {
        private final DeskId desk;
        private final Period period;
    }

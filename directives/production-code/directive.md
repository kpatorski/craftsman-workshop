---
id: production-code
title: Production code assessment
description: >
  Rules applied whenever production code is written or refactored. No imposed review order — each rule is checked on its
  own merit.
applies-when: writing or refactoring production code
composes: [visibility, naming, rich-domain, error-handling, interfaces, abstraction-timing, feature-structure,
  determinism, specifications, single-responsibility, framework-isolation, libraries-first, functional-style,
  no-explanatory-comments]
precedence: the project's existing conventions win
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Fourteen composed directives, checked on their own merit, in no particular order:

1. [visibility](../visibility/directive.md) — lowest visibility by default.
2. [naming](../naming/directive.md) — domain-language names, verb-noun use cases.
3. [rich-domain](../rich-domain/directive.md) — behaviour lives on the domain object.
4. [error-handling](../error-handling/directive.md) — results over exceptions, no internal null.
5. [interfaces](../interfaces/directive.md) — no interface without a reason.
6. [abstraction-timing](../abstraction-timing/directive.md) — stay concrete until the second use case.
7. [feature-structure](../feature-structure/directive.md) — organise by feature, not by layer.
8. [determinism](../determinism/directive.md) — no ambient time or randomness in business logic.
9. [specifications](../specifications/directive.md) — explicit business rules as Specifications.
10. [single-responsibility](../single-responsibility/directive.md) — one responsibility per class.
11. [framework-isolation](../framework-isolation/directive.md) — the domain drives the structure.
12. [libraries-first](../libraries-first/directive.md) — check for an existing library before writing a util.
13. [functional-style](../functional-style/directive.md) — functional constructs where they clarify.
14. [no-explanatory-comments](../no-explanatory-comments/directive.md) — rename and extract instead of commenting.

Enabling or disabling this directive enables or disables all fourteen together; each can still be toggled on its own.

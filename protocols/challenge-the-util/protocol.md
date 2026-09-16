---
id: challenge-the-util
title: Confirm a util is really the right home
description: >
  Confirms a util is genuinely the right home before writing one.
input: a proposed util
output: a confirmed decision to proceed with a util, or a redirect to a better home
uses: [libraries-first]
checkpoint:
  type: ask
  blocking: true
  prompt: "This could live as <alternative> instead of a util. Still want a util here?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Check the code does not belong on a domain object or use case instead.
2. Check it is not already provided by Apache Commons, Vavr, the standard library, or the framework in use — consult
   [libraries-first](../../directives/libraries-first/directive.md).
3. Stop at the checkpoint below before proceeding.

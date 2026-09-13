---
id: challenge-the-util
title: Confirm a util is really the right home
description: >
  Before writing a util, check it does not belong on a domain object or use case, and is not already provided by Apache Commons, Vavr, the standard library, or the framework in use.
input: a proposed util
output: a confirmed decision to proceed with a util, or a redirect to a better home
uses: [libraries-first]
checkpoint:
  type: ask
  blocking: true
  prompt: "This could live as <alternative> instead of a util. Still want a util here?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [scenario-utils](../scenario-utils/protocol.md).

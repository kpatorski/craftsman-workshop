---
id: confirm-conventions
title: Confirm structural conventions before creating classes
description: >
  Confirms structural conventions before creating a class.
input: the target located by locate-target
output: settled placement and naming decisions for the classes about to be created
uses: [architecture-profile, feature-structure, naming]
checkpoint:
  type: ask
  blocking: true
  when: a placement / layer / port-vs-adapter / naming decision is not already fixed by the profile or the project
  prompt: >
    About to create <class>. I'd put it in <package> as <layer role>, named <name>. Agree, or place it differently?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Settle the structural decisions a new class forces: which layer it belongs to, its package, whether it is a port or an adapter, its name per the layer's convention.
2. Decisions already determined by architecture-profile or the existing project structure are applied silently.
3. **Check whether the aggregate behind this class is already owned by another use case** (domain-design's
   `identify-aggregates` put more than one command under it) — if so, this is never a silent decision, no matter
   how settled the project's conventions otherwise are: raise it at the checkpoint below, and propose
   [feature-structure](../../directives/feature-structure/directive.md)'s resolution — this use case's own domain
   class and repository port, reading and writing the same persisted record the other use case's implementation
   already uses. Never propose reusing the other use case's class directly, and never propose a second, unrelated
   record for the same aggregate id.
4. Only genuinely open decisions are raised, at the checkpoint below.

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

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Settle the structural decisions a new class forces: which layer it belongs to, its package, whether it is a port or an adapter, its name per the layer's convention.
2. Decisions already determined by architecture-profile or the existing project structure are applied silently.
3. Only genuinely open ones are raised, at the checkpoint below.

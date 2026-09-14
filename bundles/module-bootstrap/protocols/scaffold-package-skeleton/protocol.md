---
id: scaffold-package-skeleton
title: Lay out the package skeleton
description: >
  Lays out the package skeleton from the architecture-profile and feature-structure directives.
input: the architecture-profile and feature-structure directives
output: an empty but present package skeleton
uses: [architecture-profile, feature-structure]
checkpoint:
  type: ask
  blocking: true
  prompt: "Package skeleton: <tree>. Matches how you want this module organised?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Create the top-level package structure — feature packages, shared, core, config.
2. Follow [architecture-profile](../../../../directives/architecture-profile/directive.md)
   and [feature-structure](../../../../directives/feature-structure/directive.md).
3. Empty but present — no classes yet.

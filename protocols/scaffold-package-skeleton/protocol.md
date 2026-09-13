---
id: scaffold-package-skeleton
title: Lay out the package skeleton
description: >
  Create the top-level package structure from the architecture-profile and feature-structure directives — feature packages, shared, core, config — empty but present.
input: the architecture-profile and feature-structure directives
output: an empty but present package skeleton
uses: [architecture-profile, feature-structure]
checkpoint:
  type: ask
  blocking: true
  prompt: "Package skeleton: <tree>. Matches how you want this module organised?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [bootstrap-module](../bootstrap-module/protocol.md).

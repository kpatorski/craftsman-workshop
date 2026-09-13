---
id: create-empty-package
title: Create the empty target package
description: >
  Creates the empty target package for a new use case.
input: the target package located by locate-target, and the conventions confirmed by confirm-conventions
output: an empty package ready for the suite
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Create the empty package for the new use case.
2. Mirror the structure of a sibling use case, unless this one genuinely needs a different convention.

Used by: [scenario-new-use-case](../scenario-new-use-case/protocol.md).

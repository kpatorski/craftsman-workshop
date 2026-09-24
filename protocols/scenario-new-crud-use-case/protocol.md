---
id: scenario-new-crud-use-case
title: Add a plain CRUD use case to a module
description: >
  A use case that crud-or-domain classified as plain create/read/update/delete. Built test-first like any other
  and placed by the module's own structure, but without the domain machinery: no aggregate, no value objects beyond
  validating input, no decision about where business behaviour lives — there is none.
input: a module, and a use case whose spec states `Model: crud`
output: same as tdd-loop's output — a green, refactored suite and production code for the use case
match: task is a use case whose spec states `Model: crud`
steps: [locate-target, confirm-conventions, create-empty-package, tdd-loop]
overrides:
  aggregate-design: not applicable — a crud use case has no aggregate to draw
  value-objects: relaxed — plain validated fields are enough, validated at the edge and reported as a result
  rich-domain: not applicable — a crud use case holds no business behaviour to place
done-when: tdd-loop's done-when holds
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [locate-target](../locate-target/protocol.md) — find the module to work in.
2. [confirm-conventions](../confirm-conventions/protocol.md) — settle placement and naming before creating anything.
3. [create-empty-package](../create-empty-package/protocol.md) — create the empty target package.
4. [tdd-loop](../../bundles/tdd/protocols/tdd-loop/protocol.md) — build the use case test-first.

If a rule shows up while building that is more than validation or a permission, this is not a CRUD use case any more:
stop, say so, and reclassify it per [crud-or-domain](../../directives/crud-or-domain/directive.md) before going on.

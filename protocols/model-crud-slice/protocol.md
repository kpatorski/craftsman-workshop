---
id: model-crud-slice
title: Model a plain CRUD slice
description: >
  The modelling for a slice that crud-or-domain classified as plain create/read/update/delete: the record, the
  operations on it, and the field-level rules and permissions — and nothing else. No aggregate, command, view or
  event is derived, because there is no behaviour to model.
input: the current slice from event-model.md's `## Slices`, whose model is `crud`
output: >
  the slice's entry in event-model.md's `## CRUD slices`, and — only if a rule showed it is not really CRUD — the
  slice reclassified as `domain`, named as such
match: the current slice's model is `crud`
uses: [crud-or-domain]
checkpoint:
  type: ask
  blocking: true
  when: while modelling, a rule appeared that is more than a field-level rule or a permission
  prompt: >
    This slice was classed as plain CRUD, but <the rule> depends on <the state / the other records / an outcome that
    is computed>. That is domain behaviour. Treat the slice as domain and model it with aggregates — or is that rule
    really only validation?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Name the record this slice touches and the fields it reads or writes.
2. List the operations it performs — create, read, change, delete — and who is allowed to perform each.
3. List its rules as short phrases. Only field-level rules and permissions belong here; each one is tested against
   [crud-or-domain](../../directives/crud-or-domain/directive.md).
4. If a rule fails that test, stop at the checkpoint above. On "domain", the slice's model in `## Slices` becomes
   `domain` — named as a reclassification in the log — and the slice goes to `model-slice` instead.
5. Otherwise write the slice's entry to event-model.md's `## CRUD slices` (created with the first one): the record,
   its fields, the operations, the rules and permissions, and the slice it came from. Nothing else is derived — no
   aggregate, command, view or event.

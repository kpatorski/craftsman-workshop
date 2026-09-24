---
id: crud-or-domain
title: A plain CRUD use case gets no domain modelling
description: >
  Decides, per use case, whether it carries domain behaviour or is plain create/read/update/delete. A CRUD use case
  is built without aggregates, events, read-model derivation or rich-domain ceremony; a domain one gets all of it.
  Most systems mix both, so the call is made for each use case, never for the system as a whole.
applies-when: classifying a candidate use case, or deciding how much domain modelling a slice gets
precedence: the developer's classification of a slice wins; the project's existing conventions win over both
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

A use case is either `crud` or `domain`. Decide it for each use case on its own.

**It is `crud` only when every one of these holds:**

1. It creates, reads, changes or deletes records of one kind, and does nothing else.
2. Its only rules are field-level — required, format, length, range, a uniqueness the storage enforces — and who is
   allowed to do it.
3. Its outcome is fixed by its input: no decision that depends on the current state of this or another record, and
   no computed or derived result.
4. No other use case's rule constrains the data it writes. If some other use case enforces an invariant over the
   same records, those records are aggregate data, and this use case is `domain`.
5. Nothing outside it needs to be told it happened — no event worth publishing, no follow-up somewhere else.

If any one fails, it is `domain`. When you cannot tell — a rule may be hiding in the input — ask; never guess in
either direction. Guessing `domain` builds machinery nobody needed, guessing `crud` builds a hole where a rule
should have been.

**What a `crud` use case skips:** aggregate boundaries, the command / event split, read-model derivation, value
objects beyond validating input at the edge, deciding where business behaviour lives, events between contexts. It
is not built less carefully — there is simply no behaviour to model.

**What it still gets:** the module's package structure ([feature-structure](../feature-structure/directive.md)), its
own use case class and port, a failed validation reported as a result rather than an exception
([error-handling](../error-handling/directive.md)), tests at the highest level that still reads in business
language, no ambient time or randomness ([determinism](../determinism/directive.md)), and domain-language names
([naming](../naming/directive.md)).

**Promotion.** If a domain rule turns up later — while drafting the spec, while writing tests, or because a later
use case constrains the same records — the use case becomes `domain`. Say so at the checkpoint of the step that
finds it, never silently. The modelling it skipped is then done for it, and what was already built is treated as
existing code to change, not patched in place.

## Examples

`RenameExerciseCategory` — one record, the only rule is that the name is not blank: `crud`. `ListMyPrograms` — a
read of one kind of record: `crud`. `CancelReservation` — allowed only before it starts, and frees the desk for
someone else: `domain`. `CreateProgram` when a rule limits how many programs a block may hold: `domain`, because
that rule depends on other records.

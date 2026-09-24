---
id: propose-candidate-specs
title: Turn events into an ordered list of slices
description: >
  Turns the collected events into an ordered list of candidate use cases — slices — each of which becomes one
  spec. The slices are provisional at this point: only the intent and the events it emits are known, and
  `derive-use-cases` confirms each one as a real command / aggregate / event triple when its turn comes. The order
  is settled here, with the developer, and the first slice is the one that will be judged as the example for
  everything after it.
input: >
  event-model.md's `## Events`, plus any use cases the requirements input itself already lists (imported and
  confirmed rather than re-derived)
output: >
  an ordered list of slices — candidate spec titles, each with the events it emits, a task shape and a model
  (`crud` or `domain`) — written to event-model.md's `## Slices`, all `pending`
uses: [one-task-granularity, classify-task-shape, crud-or-domain]
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Slices, in the order I would take them: <each slice on its own line — name, the events it emits, task shape,
    model (crud or domain, and why when crud), merges marked>. First: <name>, because <why it is the best example to
    judge the direction on>. Add, drop, merge, split, or reorder?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Read `event-model.md`'s `## Events` and propose one slice per task, naming each by the intent that triggers its
   events. Where the input already lists its own use cases, take them as the starting point and say so.
2. Small, tightly-coupled slices may be proposed as one merged candidate — never merged silently, always flagged
   as a proposal.
3. Classify each slice `crud` or `domain` per [crud-or-domain](../../../../directives/crud-or-domain/directive.md),
   and say why a slice is `crud`. A slice that cannot be classified from the input is asked about at the checkpoint,
   never guessed. A `crud` slice skips the domain modelling later on, so this is the one place the call is made.
4. Choose the first slice deliberately: prefer one that touches the central aggregate and exercises more than one
   kind of rule, over a trivial one — the first slice is built completely and judged as the example for all the
   rest, and a check of direction on a trivial one tells the developer very little. When every slice is `crud`, there
   is no aggregate to be central: take the one that exercises the most of the persistence path. Say why it was
   chosen; the developer can override.
5. Keep each slice to what one `implement` run can finish — every slice is modelled, specified and built
   test-first before the next begins, so an oversized one is an oversized TDD run, not just a long spec.
6. Write the confirmed list to `event-model.md` as `## Slices`, in order, each `pending` and carrying its model. Each
   entry later carries its status, its spec's path, and the commit that implemented it — see `slice-loop`.

This step does not know the aggregates yet — that is deliberate. A slice list drawn now is provisional, and a
later slice can turn out to belong with an earlier one; that is raised at the checkpoint of the step that finds
it, never absorbed silently.

---
id: derive-use-cases
title: Derive use cases from command + aggregate + event
description: >
  Derives candidate use cases from command + aggregate + event triples, merging only where one real decision
  justifies it — same aggregate alone is not that decision.
input: commands, aggregates and events from the preceding event-storming steps
output: >
  a list of candidate use cases, each tied to its command / aggregate / event triple, every merge flagged with the
  single decision that justifies it
uses: [naming]
checkpoint:
  type: notify
  prompt: >
    Use cases: <verb-noun name -> command / aggregate / event>. <Where triples were merged: the merge and the one
    caller decision that justifies it. Where a split looked mergeable: why it stayed split.> <Any process manager
    from derive-commands appears as a use case of its own.>
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Default 1:1 — one command/aggregate/event triple is one candidate use case.
2. Merge only when all three hold: same aggregate; the triples are one decision the caller makes in one
   interaction, such that issuing one without the other leaves the domain in a state nobody wants; and merging
   hides no rule — the acceptance criteria stay separately statable.
3. State the counter-criterion explicitly, because it is the mistake to guard against: same aggregate alone is
   *not* a reason to merge. That is just the aggregate's cohesion — feature-structure gives each use case its own
   class over the shared record anyway, so merging buys nothing and costs a rule's visibility.
4. Always split when the triples touch different aggregates; different actors issue them; they happen at
   different times; one is rejectable and the other is not; they sit in different bounded contexts.
5. Name it verb-noun in ubiquitous language (see [naming](../../../../directives/naming/directive.md)).
6. A process manager surfaced by [derive-commands](../derive-commands/protocol.md) is a use case in its own
   right — named with its trigger event, the command it issues, and its compensation. Never folded into either
   aggregate's use case.
7. Once confirmed, append a `## Use cases` section to `event-model.md` — each candidate with its triple and, where
   merged, the one decision that justified it.

This names *candidate* use cases; whether two candidates become one *spec* is `propose-candidate-specs`' call
under `one-task-granularity` — the criterion there is "can one implement run finish it", a different question
from "is this one operation in the domain". Never pre-merge silently.

---
id: derive-views
title: Derive the read models the use cases will need
description: >
  Derives the read models the use cases will need, and where each one reads from — the owning aggregate directly,
  a same-context query, or an eventually-consistent projection.
input: commands and events from derive-commands, marked rejectable or unconditional
output: >
  a list of views, each with its source — the owning aggregate's repository, a query over the same storage, or an
  event-fed projection — and, where the source is a projection, the staleness the business accepts
uses: [feature-structure, framework-isolation]
checkpoint:
  type: notify
  prompt: >
    Views: <view -> source, consistency>. <Any view whose reader decides whether to issue a rejectable command is
    named here together with the aggregate-side check that still enforces that rule at write time.>
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. For each command, name the read model its caller needs to decide whether to issue it; for each event, the read
   model that shows its result.
2. Pick the source from exactly three, with criteria:
   - **Read through the owning aggregate's repository** — default. Same bounded context, one aggregate's data,
     must be as fresh as the write. No extra storage, no staleness.
   - **A query over the same storage** — when the view spans several aggregates *inside one context*, or needs a
     shape the aggregate would have to be distorted to provide. Still strongly consistent. A read model is not an
     entity class and must not reuse one (see
     [feature-structure](../../../../directives/feature-structure/directive.md)), and persistence types do not
     escape it (see [framework-isolation](../../../../directives/framework-isolation/directive.md)).
   - **A separate projection with its own storage, fed by events** — when the view crosses a bounded-context
     boundary, has a radically different read shape or scale, or must survive the writer being down. This is the
     only one of the three that is eventually consistent, and choosing it obliges you to name the staleness the
     business accepts and what a stale read does. See
     [aggregate-design](../../../../directives/aggregate-design/directive.md) for the rule this follows.
3. The decisive question, stated plainly: does anyone read this view to make a decision the writer must not
   contradict? If yes, an eventually-consistent projection is not enough on its own — the rule is still enforced
   aggregate-side when the command is handled. This is the "validate on read, race on write" bug, and it is the
   payoff for the rejectable analysis in [derive-commands](../derive-commands/protocol.md) — the same discipline
   as [identify-aggregates](../identify-aggregates/protocol.md)' visibility check, one layer out.
4. A view crossing a context boundary is always eventually consistent and belongs to that pair's integration — it
   is listed at [draw-bounded-contexts](../draw-bounded-contexts/protocol.md), not invented separately here.
5. Do not invent views nobody asked for: every view traces to a command someone must decide to issue, or an
   outcome someone must see.
6. Once confirmed, append a `## Views` section to `event-model.md` — each view with its source and, where the
   source is a projection, the staleness the business accepts.

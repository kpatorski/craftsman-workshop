---
id: draw-bounded-contexts
title: Draw bounded contexts and how they communicate
description: >
  Draws bounded contexts and settles how they communicate — which context-mapping pattern governs each pair, and
  what that pattern obliges you to actually build.
input: the aggregates identified by identify-aggregates
output: >
  bounded contexts, each with its aggregates; and for each pair that must talk, the relationship — its direction,
  its context-mapping pattern, and the mechanism (domain events or a synchronous call)
uses: [architecture-profile]
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Contexts: <name -> aggregates, with the one language that makes it one context>. Between them: <upstream ->
    downstream: pattern, mechanism, and what actually gets built>. <Where the pattern was a close call, name both
    options with what each costs — e.g. (a) conformist, no translation code, your model follows theirs and moves
    when theirs moves; (b) anticorruption layer, a translating adapter to write and maintain, your model stays
    yours — and ask which.> Confirm before moving to specs?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Group aggregates by **language**, not by subject matter. The decisive signal is one word meaning two different
   things: if "Customer" means something different to two groups of events, that is a boundary, not a naming
   problem. Secondary signals, in order of strength: a term needing translation when it crosses; different
   actors/teams owning the decisions; different rates of change; different consistency requirements.
2. Re-open every split `identify-aggregates` deferred to "these belong to different bounded contexts" — that was a
   promise made before contexts existed. Confirm the contexts really do differ; if they turn out to be one
   context, the merge resolution was the right one, and that gets said out loud now, before specs are written.
3. For each pair of contexts that must talk, answer two questions first: do you control the other side (same
   team, another team, another company, or legacy nobody owns), and is translation needed (is their model good
   enough to adopt as-is)? Then name the relationship as one of these patterns, each with its trigger and its
   cost:
   - **Partnership** — the two contexts succeed or fail together; coordinated planning and releases. Cost: no
     independent release.
   - **Shared Kernel** — a small, explicitly delimited shared model both sides own; every change needs both
     sides' agreement. Only when duplication cost genuinely exceeds coordination cost. Cost: the strongest
     coupling on this list — keep it tiny or not at all.
   - **Customer/Supplier** — upstream accepts downstream's requirements into its own backlog; downstream's needs
     are negotiated and planned. Requires real organisational leverage; do not choose it wishfully.
   - **Conformist** — upstream will not accommodate you; you adopt its model verbatim, no translation. Cheap and
     correct when their model is good enough. Cost: their model's changes become your changes.
   - **Anticorruption Layer** — you translate at the boundary into your own model because theirs would corrupt
     yours: legacy, a vendor, or a model shaped by a different business. Cost: an adapter and a mapping to
     maintain, forever. The default answer for legacy and third-party integration.
   - **Open Host Service** — you are upstream to several consumers; publish one defined protocol instead of a
     bespoke integration per consumer.
   - **Published Language** — a documented, versioned interchange format (usually the domain-event schema) both
     sides code against; normally paired with Open Host Service.
   - **Separate Ways** — the integration is not worth its cost; duplicate the small thing and stop talking. A
     legitimate, under-used answer — name it when it applies.
4. Settle the mechanism — asynchronous domain events (the default
   [architecture-profile](../../../../directives/architecture-profile/directive.md) already sets between bounded
   contexts) or a synchronous call — and state the consequence explicitly: across a context boundary the data is
   eventually consistent, and the acceptable lag plus the behaviour on a stale read get named here, not assumed.
   See [aggregate-design](../../../../directives/aggregate-design/directive.md) for the rule this follows.
5. Name what actually gets built per relationship, so a spec can be written from this: Anticorruption Layer → a
   translating adapter plus your own model types inside your context; Open Host Service / Published Language → an
   event schema owned by the upstream context; Conformist → their types used at your adapter layer only, never
   past it (see [framework-isolation](../../../../directives/framework-isolation/directive.md)); Separate Ways →
   nothing, and say so.

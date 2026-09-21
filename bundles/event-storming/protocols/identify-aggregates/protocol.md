---
id: identify-aggregates
title: Group events under the aggregate that owns them
description: >
  Places the current slice's events under the aggregate that owns them — a new one, or an earlier slice's aggregate
  extended, or (named as such) revised.
input: >
  the current slice's events and their attached rules, every event collected so far, and the aggregates decided
  by earlier slices
output: the aggregate for this slice, with its owned events and rules
uses: [aggregate-design]
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Aggregate for this slice: <name -> events, with the invariant it protects; new, extended from an earlier
    slice, or a REVISION of one — say which, and what changed and why>. <If step 3's visibility check failed for
    any proposed root: name both resolutions with what each actually costs — (a) merge into <aggregate>, one true
    consistency boundary, the invariant always holds; (b) keep <name>s separate, downgrade this from an aggregate
    invariant to an application-level constraint, enforced by <mechanism — a spanning unique constraint, a
    reconciling process, or an accepted race> — and ask which.> Boundaries right?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Group this slice's events, with their rules, under the aggregate responsible for them — an aggregate decided by
   an earlier slice when it already owns the relevant invariant, otherwise a new one. This is decided one slice at
   a time, so a boundary drawn now can turn out to be wrong once a later slice arrives. When this slice's events
   belong with an earlier aggregate in a way that changes what that aggregate was confirmed to be, that is a
   **revision**: name it as one, with what changes and why, at this checkpoint. Never re-cut an earlier boundary
   silently.
2. For each aggregate, name the invariant it actually protects — the thing that must never become false, which is
   why these events belong together and nowhere else. "Owns these events" without a stated invariant is not a
   finished answer; a developer confirming boundaries needs the reasoning, not just the grouping, to catch a wrong
   split before it hardens into commands and specs.
3. Check that a single instance of the proposed aggregate can actually *see* everything the stated invariant needs —
   never assume it holds just because the events are grouped together. Check against **every** collected event and
   every aggregate decided so far, not only this slice's events: a sibling that matters may belong to a slice not
   modelled yet. The classic trap: a "no duplicate / no conflict across many instances of the same aggregate"
   invariant can't be enforced by that aggregate at all — one `Reservation` has no visibility into a sibling
   `Reservation` for the same desk and day, so it cannot be the one stopping them from coexisting.

   When this happens, there are exactly two legitimate resolutions — present both, with what each one actually
   costs, and let the developer pick; never default to either silently:
   - **Merge the boundary** to whichever aggregate *does* have the needed visibility (often the contended-for
     resource, not the thing contending for it) — one true aggregate, one consistency boundary, the invariant is
     always true. This is the right call when the events genuinely belong to one bounded context and the
     invariant must never be violated, not even briefly.
   - **Keep the aggregates separate** — a real option, not a fallback, when the proposed roots genuinely belong to
     different bounded contexts or use cases that should not be coupled into one consistency boundary. This means
     admitting the invariant is no longer an *aggregate* invariant but an application-level constraint, and naming
     what actually enforces it instead: a database-level constraint (e.g. a unique/exclusion constraint) spanning
     both, a saga or reconciling process that corrects a rare violation after the fact, or a documented, accepted
     risk of a race. Never claim this constraint "just holds" without naming the mechanism — that is the same
     mistake as claiming an aggregate protects something it structurally cannot see, one layer up.
4. Draw the aggregate boundary — whichever resolution was chosen. Keep the result small — see
   [aggregate-design](../../../../directives/aggregate-design/directive.md) for sizing and how sibling aggregates
   should be referenced.
5. Once confirmed, write this slice's aggregate into `event-model.md`'s `## Aggregates` section (create it on the
   first slice) — its owned events and the invariant it protects; a revision edits the earlier entry and marks it
   `revised at <slice>`. Same discipline as `attach-rules-batch`: written immediately, not deferred to the end.

**This boundary is a consistency guarantee, not a Java class.** "One aggregate" means one persisted record every
owning command must read and write through — it does not mean one shared domain class reused verbatim by every use
case that touches it. How that split happens in code, once several use cases share this aggregate, is
[feature-structure](../../../../directives/feature-structure/directive.md)'s call, made at
[confirm-conventions](../../../../protocols/confirm-conventions/protocol.md) — not this protocol's.

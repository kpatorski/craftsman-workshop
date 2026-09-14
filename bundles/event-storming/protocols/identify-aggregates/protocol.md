---
id: identify-aggregates
title: Group events under the aggregate that owns them
description: >
  Groups events under the aggregate that owns them.
input: events and their attached rules
output: aggregates, each with its owned events and rules
checkpoint:
  type: ask
  blocking: true
  prompt: "Aggregates: <name -> events, with the invariant each one protects>. Boundaries right?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Group events, with their rules, under the aggregate responsible for them.
2. For each aggregate, name the invariant it actually protects — the thing that must never become false, which is
   why these events belong together and nowhere else. "Owns these events" without a stated invariant is not a
   finished answer; a developer confirming boundaries needs the reasoning, not just the grouping, to catch a wrong
   split before it hardens into commands and specs.
3. Check that a single instance of the proposed aggregate can actually *see* everything the stated invariant needs —
   never assume it holds just because the events are grouped together. The classic trap: a "no duplicate / no
   conflict across many instances of the same aggregate" invariant can't be enforced by that aggregate at all — one
   `Reservation` has no visibility into a sibling `Reservation` for the same desk and day, so it cannot be the one
   stopping them from coexisting. When the invariant needs visibility the proposed root doesn't have, move the
   boundary to whichever aggregate *does* have it (often the contended-for resource, not the thing contending for
   it), or say plainly that this is an application-level uniqueness constraint, not an aggregate invariant — never
   claim an aggregate protects something it structurally cannot see.
4. Draw the aggregate boundary.

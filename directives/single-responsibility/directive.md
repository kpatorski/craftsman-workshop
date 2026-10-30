---
id: single-responsibility
title: One responsibility per class
description: >
  A class does one thing. Split by responsibility while keeping the business intent cohesive — this is SOLID's S,
  applied without ceremony.
applies-when: a class is taking on more than one concern
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- no class that validates, orchestrates, persists, logs, transforms and decides at once
- split by responsibility while keeping the business intent cohesive
- a class has one reason to change: name who would ask for a change to it — one business rule, one integration, one
  screen; two different answers mean two classes
- follow SOLID; if a rule seems to fight SOLID, redesign rather than force it through

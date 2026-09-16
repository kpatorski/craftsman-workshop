---
id: definition-of-done
title: What "done" means unless a spec says otherwise
description: >
  Mirrors, in spirit, what an `implement` procedure calls `done-when` — stated independently here since specs and the
  implementation workshop are separate, independently-installed content.
applies-when: deciding whether a spec's work is finished
precedence: a spec may state extra done-criteria explicitly and those win, on top of this default
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Default:

- all acceptance criteria are covered by passing tests
- production code is refactored, not just made to pass
- the change is committed

A spec may state extra done-criteria explicitly (e.g. "and the migration is applied in staging").

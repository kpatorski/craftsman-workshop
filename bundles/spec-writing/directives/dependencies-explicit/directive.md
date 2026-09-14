---
id: dependencies-explicit
title: State ordering dependencies between specs
description: >
  A spec that silently assumes another one is already done breaks the moment specs are picked up out of order.
applies-when: drafting a spec that needs another spec's work done first
precedence: none — this always applies
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- if spec B needs spec A done first, B's `depends-on` lists A's id
- never rely on file order or numbering alone to imply a dependency

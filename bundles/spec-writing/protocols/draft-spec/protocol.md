---
id: draft-spec
title: Draft one spec
description: >
  Drafts one spec from an accepted candidate, applying spec-rules.
input: the current slice — one candidate from propose-candidate-specs — with its modelling already in event-model.md
output: a spec file in specs/, not yet final
uses: [spec-rules]
checkpoint:
  type: ask
  blocking: true
  prompt: "Spec <n> <title>: <scope + acceptance criteria as drafted>. Change anything?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Write Context / Acceptance criteria / Out of scope / Open questions for one candidate. State the slice's model
   (`Model: crud` or `Model: domain`, from `## Slices`) on the line under the title — `implement` reads it to pick
   its scenario.
2. Apply [spec-rules](../../directives/spec-rules/directive.md) throughout.

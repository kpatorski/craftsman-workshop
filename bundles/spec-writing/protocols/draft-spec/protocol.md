---
id: draft-spec
title: Draft one spec
description: >
  Drafts one spec from an accepted candidate, applying spec-rules.
input: one accepted candidate from propose-candidate-specs
output: a spec file in specs/, not yet final
uses: [spec-rules]
checkpoint:
  type: ask
  blocking: true
  prompt: "Spec <n> <title>: <scope + acceptance criteria as drafted>. Change anything?"
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Write Context / Acceptance criteria / Out of scope / Open questions for one candidate.
2. Apply [spec-rules](../../directives/spec-rules/directive.md) throughout.

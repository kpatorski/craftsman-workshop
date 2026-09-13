---
id: draft-spec
title: Draft one spec
description: >
  Write Context / Acceptance criteria / Out of scope / Open questions for one candidate, applying spec-rules.
input: one accepted candidate from propose-candidate-specs
output: a spec file in specs/, not yet final
uses: [spec-rules]
checkpoint:
  type: ask
  blocking: true
  prompt: "Spec <n> <title>: <scope + acceptance criteria as drafted>. Change anything?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [detail-spec](../detail-spec/protocol.md).

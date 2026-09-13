---
id: detail-spec
title: Draft each accepted candidate spec
description: >
  One pass per accepted candidate, drafting its spec and stopping for review before the next.
input: the accepted candidate list from propose-candidate-specs
output: every accepted candidate has a reviewed, written spec file
steps: [draft-spec]
repeat-until: every accepted candidate has a reviewed, written spec file
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). Replaces the old `loop` kind — see `repeat-until`.

## Protocol

Repeat until the condition holds:

1. [draft-spec](../draft-spec/protocol.md)

Used by: [requirements-analysis](../requirements-analysis/protocol.md).

---
id: restate-understanding
title: Restate what needs to be done
description: >
  Summarise, in the product owner's language, what the input is asking for, before running any analysis.
input: the input read by ingest
output: a confirmed summary of what needs doing
checkpoint:
  type: ask
  blocking: true
  prompt: "Here's what I understand needs doing: <summary>. Correct?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [requirements-analysis](../requirements-analysis/protocol.md).

---
id: restate-current-behaviour
title: Restate what the code currently does
description: >
  Summarise the current behaviour in the product owner's language. Usually an internal step; it becomes a checkpoint only when the behaviour is tangled or ambiguous.
input: the existing tests and code read by read-existing-tests
output: an agreed baseline of current behaviour
checkpoint:
  type: ask
  when: the current behaviour is tangled or ambiguous
  prompt: "Current behaviour as I read it: <summary>. Correct baseline before I change it?"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [scenario-change-existing-code](../scenario-change-existing-code/protocol.md).

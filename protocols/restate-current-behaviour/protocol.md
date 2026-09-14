---
id: restate-current-behaviour
title: Restate what the code currently does
description: >
  States what the code currently does, in the product owner's language.
input: the existing tests and code read by read-existing-tests
output: an agreed baseline of current behaviour
checkpoint:
  type: ask
  when: the current behaviour is tangled or ambiguous
  prompt: "Current behaviour as I read it: <summary>. Correct baseline before I change it?"
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Summarise the current behaviour in the product owner's language.
2. Usually internal; becomes a checkpoint only when the behaviour is tangled or ambiguous.

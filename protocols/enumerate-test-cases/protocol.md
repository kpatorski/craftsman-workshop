---
id: enumerate-test-cases
title: List every known test case as a failing stub
description: >
  Lists every known test case as a failing stub, before any implementation.
input: the empty suite from scaffold-suite, and the behaviour's known business cases
output: one failing stub per known business case, no bodies
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Here is the full list of test cases. Complete and correct — anything to add, drop, or rename?
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Write down every business case discovered so far as an empty, failing stub — a titled test that just fails.
2. The title states the scenario in the product owner's language.
3. Nothing is implemented yet; the goal is a complete map of what the suite must prove.

## Examples

    def "event is published if reservation succeed"() {
      expect:
      false
    }

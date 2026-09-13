---
id: enumerate-test-cases
title: List every known test case as a failing stub
description: >
  Write down every business case discovered so far as an empty, failing stub — a titled test that just fails. The title states the scenario in the product owner's language. Nothing is implemented yet; the goal is a complete map of what the suite must prove.
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

Used by: [tdd-loop](../tdd-loop/protocol.md). [scenario-change-existing-code](../scenario-change-existing-code/protocol.md) overrides it — means adding stubs or assertions to the existing suite, following its convention, not starting a new one.

## Examples

    def "event is published if reservation succeed"() {
      expect:
      false
    }

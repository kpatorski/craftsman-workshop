---
id: scaffold-suite
title: Create the empty test suite
description: >
  Create the test file(s) for the chosen level. Shape depends on the level: one suite per production class, one suite per use-case entry point, or several suites targeting the same entry point when corner cases would otherwise bloat a single suite.
input: the test level chosen by decide-test-level
output: empty test file(s), no cases yet
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Create one file per the chosen level's shape. No cases, no assertions yet — that is enumerate-test-cases' job.

---
id: commit-tests
title: Commit the tests on their own
description: >
  Commits the characterization tests on their own, once finish-characterize is approved.
input: the approved characterization tests from finish-characterize
output: a separate commit containing only the added tests
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Runs only after finish-characterize is approved.
2. Commit the characterization tests as a standalone commit — never folded into an unrelated change.

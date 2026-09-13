---
id: commit-tests
title: Commit the tests on their own
description: >
  Runs only after finish-characterize is approved. The characterization tests land as a standalone commit — never folded into an unrelated change.
input: the approved characterization tests from finish-characterize
output: a separate commit containing only the added tests
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [characterize-loop](../characterize-loop/protocol.md).

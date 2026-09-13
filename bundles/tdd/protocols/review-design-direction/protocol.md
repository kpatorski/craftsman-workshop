---
id: review-design-direction
title: Confirm the design direction before the next batch
description: >
  Confirms the design direction before the next coverage batch.
input: the test and production diffs from the current cover-cycle iteration
output: a shared decision to continue as-is or adjust the design
uses: [how-high-to-test]
checkpoint:
  type: ask
  blocking: true
  shows: [test-diff, production-diff]
  prompt: >
    This batch added <APIs / signatures>. I think it is going <well / off> because <reason>. Continue to the next
    batch, or adjust first? (If the suite is starting to bloat with corner cases, I'll also flag re-picking the test
    level per how-high-to-test.)
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Look at what the batch introduced — interfaces, public / package-private API, method and parameter names.
2. State whether it is heading the right way, and why.

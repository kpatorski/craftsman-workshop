---
id: minimal-production-code
title: Write the least production code that makes the batch pass
description: >
  Implement only what makes the current batch green. No speculative structure. If writing it reveals a new case, add a failing stub for it right away and carry on.
input: the current batch of test bodies from cover-batch
output: production code making the current batch pass; suite green for covered stubs
uses: [production-code]
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

Apply the [production-code](../../../../directives/production-code/directive.md) directive while writing. A newly discovered
case gets a failing stub immediately — that feeds back into the current cover-cycle iteration, not a derailment.

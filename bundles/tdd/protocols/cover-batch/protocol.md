---
id: cover-batch
title: Implement bodies for a small batch of stubs
description: >
  Take 2-3 stubs — few enough that the production code to satisfy them is a short step — and write their bodies. Tests only; production code is the next step.
input: the stub list from enumerate-test-cases
output: implemented bodies for the current batch
uses: [stub-vs-in-memory]
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

Consult [stub-vs-in-memory](../../../testing/directives/stub-vs-in-memory/directive.md) whenever a batch needs a fake
for a
collaborator.

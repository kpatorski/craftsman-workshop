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

1. Consult [stub-vs-in-memory](../../../testing/directives/stub-vs-in-memory/directive.md) whenever a batch needs
   a fake for a collaborator.
2. Write bodies only — real assertions against the production API this batch needs, but not the production code
   itself. If that API doesn't exist yet, the body references something that isn't there yet; that's expected.
3. **Run the suite and confirm this batch is actually red before moving on** — a compile failure because the
   production code doesn't exist yet counts as red, not as a problem to fix here. This is not optional and not
   implied by "tests only" above: writing a body and *believing* it would fail is not the same as watching it
   fail. Skipping this and going straight to `minimal-production-code` collapses TDD into "write code with tests
   attached" — the failure this step exists to catch is a body that doesn't actually exercise what you think it
   does, discovered only by writing the implementation and finding the test was already accidentally green, or
   would have passed against a *wrong* implementation.

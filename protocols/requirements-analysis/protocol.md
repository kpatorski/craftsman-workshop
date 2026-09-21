---
id: requirements-analysis
title: Requirements analysis loop
description: >
  Turns a requirements input into reviewed specs and working code. Every event is collected first, for the whole
  input — cheap, and it gives the Big Picture. After that the work goes one slice (one candidate use case) at a
  time, each carried from rules to a reviewed spec to an implemented, committed use case and a direction check
  before the next begins, so the developer can judge the approach on the first working example and never has to
  hold the whole system in their head.
input: the input read by ingest
output: reviewed, written spec files, a current specs/README.md, and each spec's use case implemented and committed
steps: [restate-understanding, collect-events, propose-candidate-specs, slice-loop, draw-bounded-contexts,
  collect-open-questions, finalize]
done-when: >
  every slice has a reviewed spec and its use case implemented and committed, every blocking open question is
  resolved or left explicitly `status: blocked`, and specs/README.md is current
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [restate-understanding](../restate-understanding/protocol.md)
2. [collect-events](../../bundles/event-storming/protocols/collect-events/protocol.md)
3. [propose-candidate-specs](../../bundles/spec-writing/protocols/propose-candidate-specs/protocol.md) — turns the
   events into an ordered list of slices.
4. [slice-loop](../slice-loop/protocol.md) — one slice at a time: model it, draft its spec, implement it, confirm
   the direction.
5. [draw-bounded-contexts](../../bundles/event-storming/protocols/draw-bounded-contexts/protocol.md) — after every
   slice, because it needs all the aggregates.
6. [collect-open-questions](../../bundles/spec-writing/protocols/collect-open-questions/protocol.md)
7. [finalize](../../bundles/spec-writing/protocols/finalize/protocol.md)

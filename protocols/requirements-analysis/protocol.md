---
id: requirements-analysis
title: Requirements analysis loop
description: >
  Turns a requirements input into reviewed, written spec files — event storming for the analysis itself, then one spec per accepted candidate.
input: the input read by ingest
output: reviewed, written spec files and a current specs/README.md
steps: [restate-understanding, event-storming, propose-candidate-specs, detail-spec, collect-open-questions, finalize]
done-when: "every accepted candidate has a spec file, every blocking open question is resolved or left explicitly `status: blocked`, and specs/README.md is current"
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. [restate-understanding](../restate-understanding/protocol.md)
2. [event-storming](../../bundles/event-storming/protocols/event-storming/protocol.md)
3. [propose-candidate-specs](../../bundles/spec-writing/protocols/propose-candidate-specs/protocol.md)
4. [detail-spec](../../bundles/spec-writing/protocols/detail-spec/protocol.md)
5. [collect-open-questions](../../bundles/spec-writing/protocols/collect-open-questions/protocol.md)
6. [finalize](../../bundles/spec-writing/protocols/finalize/protocol.md)

---
id: digest-requirements
title: Digest raw requirements into Given/When/Then business rules
description: >
  Reads the raw input and extracts the business rules it implies, as Given/When/Then statements, grouped by the
  section/story fragment they came from. No domain modelling here — no events, aggregates, or contexts; that is a
  downstream concern. Purely: prose in, structured rules out.
input: raw input text, split into sections, from read-input
output: >
  every section has its rules extracted and triaged, business-rules.md holds the cited ones, and
  open-questions.md (if anything was parked) holds the rest
steps: [extract-rules, finalize-digest]
done-when: >
  every section has its rules extracted and triaged, business-rules.md holds the cited ones, and
  open-questions.md (if anything was parked) holds the rest
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [extract-rules](../extract-rules/protocol.md)
2. [finalize-digest](../finalize-digest/protocol.md)

---
id: digest-requirements
title: Digest raw requirements into Given/When/Then business rules
description: >
  Reads the raw input and extracts the business rules it implies, as Given/When/Then statements, grouped by the section/story fragment they came from. No domain modelling here — no events, aggregates, or contexts; that is a downstream concern. Purely: prose in, structured rules out.
input: raw input text, split into sections, from read-input
output: every section has its rules extracted and confirmed, and the rules file is written
steps: [extract-rules, finalize-digest]
done-when: every section has its rules extracted and confirmed, and the rules file is written
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [extract-rules](../extract-rules/protocol.md)
2. [finalize-digest](../finalize-digest/protocol.md)

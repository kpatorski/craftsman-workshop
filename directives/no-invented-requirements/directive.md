---
id: no-invented-requirements
title: Unknowns go to Open questions, never guessed
description: >
  A spec's job is to be trustworthy input for `implement` — a guessed requirement defeats that.
applies-when: drafting a spec, or any point a business rule or constraint is missing from the input
precedence: none — this always applies
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- never fabricate a business rule, a value, or a constraint not present in the input or confirmed by the developer
- an unresolved unknown blocking the spec sets `status: blocked` and lists the question under Open questions

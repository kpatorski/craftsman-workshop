---
id: classify-task-shape
title: Classify the shape of a candidate task
description: >
  A tool-agnostic hint carried in a spec's `shape` field. `domain-design` does not assume any downstream tool exists — it names the kind of change, not a scenario id belonging to something else. If `implement` (or another tool) is also installed, map these shapes to its own scenarios yourself: new-module -> a bootstrap-style scenario, new-behaviour -> an add-use-case-style scenario, change-behaviour -> a modify-existing-code-style scenario, coverage-only -> a backfill-tests-style scenario.
applies-when: proposing a candidate spec, in `propose-candidate-specs`
precedence: none — this is a classification, not a convention to override
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

- If the use case's bounded context is not yet an existing module → `new-module`.
- If the use case is new behaviour in a module that already exists → `new-behaviour`.
- If the use case changes behaviour of existing, tested code → `change-behaviour`.
- If the task is purely adding missing test coverage, no behaviour change → `coverage-only`.

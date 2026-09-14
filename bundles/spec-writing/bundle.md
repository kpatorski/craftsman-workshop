---
id: spec-writing
title: Turn accepted use cases into written task specs
description: >
  Turns a list of use cases into candidate specs, drafts each accepted one to a self-contained format — acceptance
  criteria, a definition of done, explicit dependencies — and closes the run with every open question surfaced
  rather than guessed.
---

## Schema

No fields of its own — see `core.md`.

## Bundle

Input is a list of use cases, each already tied to a command, an aggregate, and an event — event storming's output,
whatever produced it. This bundle does not depend on any one source for that list, only on its shape.

## Protocols

**Enabled**

| No | Id                                                                       | Title                                     |
|----|--------------------------------------------------------------------------|-------------------------------------------|
| 1  | [propose-candidate-specs](protocols/propose-candidate-specs/protocol.md) | Turn use cases into a candidate spec list |
| 2  | [detail-spec](protocols/detail-spec/protocol.md)                         | Draft each accepted candidate spec        |
| 3  | [draft-spec](protocols/draft-spec/protocol.md)                           | Draft one spec                            |
| 4  | [collect-open-questions](protocols/collect-open-questions/protocol.md)   | Surface every unresolved open question    |
| 5  | [finalize](protocols/finalize/protocol.md)                               | Write the specs and close the run         |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

**Enabled**

| No | Id                                                                               | Title                                                              |
|----|----------------------------------------------------------------------------------|--------------------------------------------------------------------|
| 1  | [classify-task-shape](directives/classify-task-shape/directive.md)               | Classify the shape of a candidate task                             |
| 2  | [one-task-granularity](directives/one-task-granularity/directive.md)             | One spec is one thing a single implement run can finish            |
| 3  | [spec-rules](directives/spec-rules/directive.md)                                 | How a spec is written                                              |
| 4  | [acceptance-criteria-format](directives/acceptance-criteria-format/directive.md) | Acceptance criteria are the Given/When/Then rules, carried through |
| 5  | [definition-of-done](directives/definition-of-done/directive.md)                 | What "done" means unless a spec says otherwise                     |
| 6  | [no-invented-requirements](directives/no-invented-requirements/directive.md)     | Unknowns go to Open questions, never guessed                       |
| 7  | [dependencies-explicit](directives/dependencies-explicit/directive.md)           | State ordering dependencies between specs                          |

**Disabled**

Empty — every one of these is stack-agnostic, none needed `enabled-by-default: false`.

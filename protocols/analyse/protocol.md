---
id: analyse
title: Turn raw requirements into Given/When/Then business rules
description: >
  Entry point for turning raw requirements prose into structured business rules — pure extraction, no domain modelling
  (no events, aggregates, contexts; that is `domain-design`'s job). There is only ever one path here, nothing to
  dispatch between. Never references an id from any other workshop content; its output is plain structured data any
  downstream reader can consume without `analyse` knowing that reader exists.
input: "a requirements input (file, URL, or inline text), plus optionally `style=<name|path>` / `session=<path>`"
output: >
  `business-rules.md`, grouped by section, ready for `domain-design` or any other reader; plus
  `open-questions.md` when any candidate could not be tied to a stated business reason
entry-point: true
steps: [read-input, digest-requirements]
done-when: digest-requirements's done-when holds
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [read-input](../read-input/protocol.md) — read the input and split it into sections.
2. [digest-requirements](../../bundles/gwt-digest/protocols/digest-requirements/protocol.md) — extract and triage
   Given/When/Then rules section by section, writing the cited ones and parking the rest.

Session file handling, directive loading, and resuming are the execution mechanics described in the `craftsman` skill
itself, not repeated per protocol — see [implement](../implement/protocol.md) for the same note.

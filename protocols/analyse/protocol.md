---
id: analyse
title: Turn raw requirements into Given/When/Then business rules
description: >
  Entry point for turning raw requirements prose into structured business rules — pure extraction, no domain modelling (no events, aggregates, contexts; that is `domain-design`'s job). Migrated from the `digester` skill's `SKILL.md` and its single `scenario-digest-input`, retired here as a separate file because there was only ever one path — nothing to dispatch between. Never references an id from any other workshop content; its output is plain structured data any downstream reader can consume without `analyse` knowing that reader exists.
input: "a requirements input (file, URL, or inline text), plus optionally `style=<name|path>` / `session=<path>`"
output: "`business-rules.md`, grouped by section, ready for `domain-design` or any other reader"
entry-point: true
steps: [read-input, digest-requirements]
done-when: digest-requirements's done-when holds
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. [read-input](../read-input/protocol.md) — read the input and split it into sections.
2. [digest-requirements](../../bundles/gwt-digest/protocols/digest-requirements/protocol.md) — extract Given/When/Then rules section by section, write
   the rules file.

Session file handling, directive loading, and resuming are the execution mechanics described in the `craftsman` skill
itself, not repeated per protocol — see [implement](../implement/protocol.md) for the same note.

---
id: spec-rules
title: How a spec is written
description: >
  Keeps specs sharp enough for `implement` to act on without re-asking what "done" means.
applies-when: drafting or reviewing a spec file, in `draft-spec`
composes: [acceptance-criteria-format, definition-of-done, no-invented-requirements, dependencies-explicit]
precedence: none — this always applies to a spec file
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

1. [acceptance-criteria-format](../acceptance-criteria-format/directive.md) — acceptance criteria are the
   Given/When/Then rules, carried through.
2. [definition-of-done](../definition-of-done/directive.md) — what "done" means unless the spec says otherwise.
3. [no-invented-requirements](../no-invented-requirements/directive.md) — unknowns go to Open questions, never guessed.
4. [dependencies-explicit](../dependencies-explicit/directive.md) — state ordering dependencies between specs.

Enabling or disabling this directive enables or disables all four together; each can still be toggled on its own.

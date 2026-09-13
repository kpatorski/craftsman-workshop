---
id: no-explanatory-comments
title: Rename and extract instead of commenting
description: >
  A comment explaining how confusing code works is a fix applied to the wrong place — rename, extract, or simplify the code instead.
applies-when: about to write a comment explaining what code does
precedence: the project's existing convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- no comments that explain how confusing code works — rename, extract, simplify instead

Allowed: legal headers, public API docs where genuinely needed, non-obvious external constraints, explicitly-requested actionable TODOs.

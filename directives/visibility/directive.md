---
id: visibility
title: Lowest visibility by default
description: >
  Classes and methods stay package-private unless they are genuinely part of the cross-module communication API.
applies-when: choosing the visibility of a class, method, or field
precedence: the project's existing visibility convention wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Must:

- classes and methods are package-private unless part of the cross-module communication API
- never expose mutable collections — return a copy or an unmodifiable view
- never leak framework or persistence types through a domain contract

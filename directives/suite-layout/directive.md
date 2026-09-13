---
id: suite-layout
title: Tests on top, helpers at the bottom
description: >
  Test methods sit at the top of the class; helper methods (stubbing, asserting, building) sit at the bottom. The reader meets the business rules first. This is deliberately unlike production-code ordering.
applies-when: laying out a test class
precedence: the project's existing file layout wins
enabled-by-default: true
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Directive

Test methods first, in the order a reader should meet them. Helper methods — stubbing, asserting, building — after, in whatever order groups them sensibly. A reader scanning top to bottom sees the requirements before the machinery.

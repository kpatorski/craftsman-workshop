---
id: module-bootstrap
title: Found a new project or module
description: >
  Agrees the stack from task requirements, creates the build, adds the agreed dependencies, lays out the package
  skeleton and baseline configuration, and picks the first aggregate to implement. The one-time setup a brand new
  module needs before any use case can be written test-first.
---

## Schema

No fields of its own — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Bundle

Input is a task that names or implies "start something new" rather than "change something existing" — no target
to locate, nothing to scaffold around. Output is a buildable, empty module: dependencies resolved, package layout
in place, ready for its first use case.

`choose-stack` is the one blocking checkpoint in this bundle: it derives stack candidates from the task's own
requirements first, and only lets an enabled `prefer-*` directive break a genuine tie between comparable
candidates — never let a preference pre-decide the stack.

## Protocols

**Enabled**

| No | Id                                                                           | Title                                 |
|----|------------------------------------------------------------------------------|---------------------------------------|
| 1  | [bootstrap-module](protocols/bootstrap-module/protocol.md)                   | Module bootstrap                      |
| 2  | [choose-stack](protocols/choose-stack/protocol.md)                           | Agree the stack                       |
| 3  | [create-build](protocols/create-build/protocol.md)                           | Create the build                      |
| 4  | [add-dependencies](protocols/add-dependencies/protocol.md)                   | Add the agreed dependencies           |
| 5  | [scaffold-package-skeleton](protocols/scaffold-package-skeleton/protocol.md) | Lay out the package skeleton          |
| 6  | [base-configuration](protocols/base-configuration/protocol.md)               | Add baseline configuration            |
| 7  | [pick-first-aggregate](protocols/pick-first-aggregate/protocol.md)           | Pick the first aggregate to implement |
| 8  | [scenario-bootstrap-module](protocols/scenario-bootstrap-module/protocol.md) | Found a new project or module         |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

None. Every structural rule this bundle applies (`architecture-profile`, `feature-structure`) stays fundament —
a new module follows the same conventions an existing one would.

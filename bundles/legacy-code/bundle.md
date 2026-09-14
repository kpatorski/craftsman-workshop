---
id: legacy-code
title: Characterization test loop
requires: [testing, tdd]
description: >
  Locks in what the code already does before changing it: read the existing code to list the cases it already
  handles, write a characterization test per case in small batches, commit the tests on their own, then close the
  loop. No behaviour changes here — that is a separate pass once the suite exists.
---

## Schema

No fields of its own — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Bundle

Input is existing code with no suite, or a suite too thin to change the code safely. Output is a suite that proves
current behaviour, committed on its own so a later behaviour change diffs cleanly against it. `requires:
[testing, tdd]`: the suite this loop produces must satisfy the same suite-shape rules as any other (`testing`),
and `characterize-loop` reuses `tdd`'s own `decide-test-level` and `scaffold-suite` rather than duplicating them —
the same case-map-first shape, applied to code that already exists instead of a behaviour being built.

## Protocols

**Enabled**

| No | Id                                                                           | Title                                              |
|----|------------------------------------------------------------------------------|----------------------------------------------------|
| 1  | [characterize-loop](protocols/characterize-loop/protocol.md)                 | Characterization test loop                         |
| 2  | [characterize-cycle](protocols/characterize-cycle/protocol.md)               | Characterization batch cycle                       |
| 3  | [characterize-batch](protocols/characterize-batch/protocol.md)               | Lock in current behaviour for a small batch        |
| 4  | [enumerate-cases-from-code](protocols/enumerate-cases-from-code/protocol.md) | Read the code to list the cases it already handles |
| 5  | [finish-characterize](protocols/finish-characterize/protocol.md)             | Close the characterization loop                    |
| 6  | [commit-tests](protocols/commit-tests/protocol.md)                           | Commit the tests on their own                      |
| 7  | [scenario-missing-tests](protocols/scenario-missing-tests/protocol.md)       | Cover existing code that lacks tests               |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

None. Every rule this bundle applies belongs to `testing` or stays fundament — characterizing existing code follows
the same suite-shape and production-code rules as writing it test-first.

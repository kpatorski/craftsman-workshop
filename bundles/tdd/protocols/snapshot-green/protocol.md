---
id: snapshot-green
title: Snapshot the green suite before refactoring
description: >
  Once the whole suite is green, take a snapshot so the refactor is reversible without disturbing the working tree —
  `git stash create` + `git stash store` (snapshot, not a revert; the tree stays intact for refactor-tests). A real
  checkpoint commit only if the developer asks for one.
input: a fully green suite
output: a restore point with all tests passing, working tree unchanged
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

`git stash create` then `git stash store` — never a plain `git stash`, which would touch the working tree.

**No prior commit exists yet** (the repo has no `HEAD` — the normal state for the very first TDD cycle right after
`bootstrap-module`, not an edge case): `git stash create` has nothing to diff against and fails outright. There is
no way to snapshot without history to snapshot *onto*, so make a real initial commit instead — it serves as the
restore point directly. This is still a git commit, so the usual blocking checkpoint applies (`EXECUTION.md`,
"Checkpoint protocol" — every checkpoint before a git commit is blocking); it does not become silent just because
it is a fallback rather than the usual path.

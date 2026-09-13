---
id: snapshot-green
title: Snapshot the green suite before refactoring
description: >
  Once the whole suite is green, take a snapshot so the refactor is reversible without disturbing the working tree — `git stash create` + `git stash store` (snapshot, not a revert; the tree stays intact for refactor-tests). A real checkpoint commit only if the developer asks for one.
input: a fully green suite
output: a restore point with all tests passing, working tree unchanged
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

`git stash create` then `git stash store` — never a plain `git stash`, which would touch the working tree.

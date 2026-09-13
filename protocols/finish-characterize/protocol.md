---
id: finish-characterize
title: Close the characterization loop
description: >
  Closes the characterization loop and confirms it is ready to commit.
input: the completed batch of characterization tests
output: a confirmed, ready-to-commit set of characterization tests
checkpoint:
  type: ask
  blocking: true
  shows: [test-diff, file-list]
  prompt: >
    Characterization done: <summary of cases + files>. Parked: <list or none>. Commit these tests as a standalone
    commit, or more first?
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Show the added tests and the files touched.
2. Confirm every observed path is covered.
3. Surface anything parked — other uncovered code, suspected bugs.
4. Set the session's Next line.

Used by: [characterize-loop](../characterize-loop/protocol.md).

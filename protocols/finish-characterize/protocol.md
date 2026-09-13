---
id: finish-characterize
title: Close the characterization loop
description: >
  Show the added tests and the files touched, confirm every observed path is covered, surface anything parked (other uncovered code, suspected bugs), and get the go-ahead to commit. Sets the session's Next line.
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

Used by: [characterize-loop](../characterize-loop/protocol.md).

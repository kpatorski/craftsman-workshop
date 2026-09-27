---
id: scenario-readme
title: Write or rework the README
description: >
  The on-demand path to a README: write one for a project that has none, or bring an existing one in line with the
  readme directive — no code change around it.
input: a task asking for the project's README.md to be written, reworked, or checked
output: same as write-readme's output — README.md written or updated and confirmed
match: task is to write, rework, or check the project's README.md, with no code change
steps: [write-readme]
done-when: write-readme's checkpoint is answered and the file is written
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [write-readme](../write-readme/protocol.md)

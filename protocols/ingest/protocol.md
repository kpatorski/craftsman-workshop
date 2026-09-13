---
id: ingest
title: Read the input
description: >
  Load the requirements input — a local .md file, a URL (fetched), or inline text given with the invocation. Also look for a `business-rules.md` (path given explicitly, or sitting next to the input) — if present, load it too; its Given/When/Then rules are authoritative input for the rest of the loop, not something to re-derive.
input: a file path, URL, or inline text
output: the raw input text, plus the digested rules if a business-rules.md was found, with sources recorded for the session file
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [domain-design](../domain-design/protocol.md).

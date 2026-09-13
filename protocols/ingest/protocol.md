---
id: ingest
title: Read the input
description: >
  Reads the requirements input, and any business-rules.md alongside it, before any analysis begins.
input: a file path, URL, or inline text
output: the raw input text, plus the digested rules if a business-rules.md was found, with sources recorded for the session file
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Load the input: a local `.md` file, a URL (fetched), or inline text given with the invocation.
2. Look for a `business-rules.md` — a path given explicitly, or a file sitting next to the input. If found, load it too.
3. A found `business-rules.md`'s Given/When/Then rules are authoritative input for the rest of the loop — carry them through as-is, do not re-derive them from the raw text.

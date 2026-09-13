---
id: read-input
title: Read the input
description: >
  Load the requirements input — a local .md file, a URL (fetched), or inline text given with the invocation. Identify its sections (headings, or natural paragraph/story breaks) — these drive the extraction batches. Parallel to `domain-design`'s `ingest`, kept as a separate file deliberately — `analyse` must stay installable and runnable with nothing else present.
input: a file path, URL, or inline text
output: raw input text, split into sections
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [analyse](../analyse/protocol.md).

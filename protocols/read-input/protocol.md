---
id: read-input
title: Read the input
description: >
  Reads the requirements input and splits it into sections.
input: a file path, URL, or inline text
output: raw input text, split into sections
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Load the input: a local `.md` file, a URL (fetched), or inline text given with the invocation.
2. Identify its sections — headings, or natural paragraph/story breaks. These drive the extraction batches.

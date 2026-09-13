---
id: create-build
title: Create the build
description: >
  Sets up the build tool for the agreed stack.
input: the stack agreed by choose-stack
output: a compiling empty project
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Set up the build tool — parent / plugin config, language version.
2. Apply any baseline tool configuration the stack's enabled preferences call for.

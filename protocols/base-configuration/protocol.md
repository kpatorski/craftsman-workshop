---
id: base-configuration
title: Add baseline configuration
description: >
  The always-needed config: a Clock bean (per the determinism directive), environment-based secrets, a schema-migration baseline if prefer-liquibase-owned-schema is enabled, a dev profile. Nothing feature-specific.
input: the compiling empty project from create-build and add-dependencies
output: a runnable module with baseline config
uses: [determinism]
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [bootstrap-module](../bootstrap-module/protocol.md).

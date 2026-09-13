---
id: base-configuration
title: Add baseline configuration
description: >
  Adds the baseline configuration every module needs, nothing feature-specific.
input: the compiling empty project from create-build and add-dependencies
output: a runnable module with baseline config
uses: [determinism]
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Add a Clock bean, per the [determinism](../../../../directives/determinism/directive.md) directive.
2. Add environment-based secrets configuration.
3. If [prefer-liquibase-owned-schema](../../../../directives/prefer-liquibase-owned-schema/directive.md) is enabled, add a schema-migration baseline.
4. Add a dev profile.
5. Nothing feature-specific belongs here.

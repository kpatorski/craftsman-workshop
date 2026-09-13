---
id: prefer-liquibase-owned-schema
title: Liquibase owns the schema, Hibernate never generates DDL
description: >
  Schema changes are explicit, versioned Liquibase changesets, never inferred by Hibernate at startup. Split out from the old `default-stack` reference so it can be toggled independently of the rest of the JVM stack.
applies-when: a persistence entity is added or changed on a project using Hibernate
precedence: the project's existing schema-management convention wins
enabled-by-default: false
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md). `enabled-by-default: false`
because this names concrete infrastructure — see core.md, "Fields specific to `directive`".

## Directive

Must:

- every schema change is a Liquibase changeset, reviewed like any other code change
- `hibernate.hbm2ddl.auto` is `none` — Hibernate never generates or alters DDL
- PostgreSQL is the target database

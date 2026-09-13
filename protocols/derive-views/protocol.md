---
id: derive-views
title: Derive the read models the use cases will need
description: >
  For each command/event pair, name the read model a caller would need to decide whether to issue that command, or to see its result.
input: commands and events from derive-commands
output: a list of views/read models
checkpoint:
  type: notify
  prompt: "Views derived: <list>."
---

## Schema

Introduces no new fields — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Protocol

Used by: [event-storming](../event-storming/protocol.md).

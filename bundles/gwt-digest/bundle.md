---
id: gwt-digest
title: Extract Given/When/Then rules from raw requirements
description: >
  Turns a prose requirements input into a `business-rules.md` file of Given/When/Then rules, section by section,
  with a checkpoint after each batch.
---

## Schema

No fields of its own — see [core.md](../../../craftsman/plugins/craftsman/core.md).

## Bundle

This is pure extraction, not modelling: no aggregates, no domain design, just reading a section and stating the
rules it already contains as Given/When/Then. Input is already-read, section-split text; output is a written
`business-rules.md`.

## Protocols

**Enabled**

| No | Id                                                               | Title                                                       | Note    |
|----|------------------------------------------------------------------|-------------------------------------------------------------|---------|
| 1  | [digest-requirements](protocols/digest-requirements/protocol.md) | Digest raw requirements into Given/When/Then business rules |         |
| 2  | [extract-rules](protocols/extract-rules/protocol.md)             | Extract rules section by section                            | repeats |
| 3  | [extract-rules-batch](protocols/extract-rules-batch/protocol.md) | Extract GWT rules for one section                           |         |
| 4  | [finalize-digest](protocols/finalize-digest/protocol.md)         | Write the rules file                                        |         |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

None. Every rule about GWT wording belongs to `testing` or stays fundament, not to this bundle.

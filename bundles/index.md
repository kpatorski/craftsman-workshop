---
name: bundles-index
description: >
  Lookup table for every bundle in this workshop — named groups of directives and protocols that install and
  enable together. `craftsman search` and `craftsman list bundle` read this first.
---

## Schema

No fields of its own beyond `Sources` below. `id`, `title`, `description`, `requires` are defined once in
`core.md` — every bundle's own `## Schema` section links back there
instead of repeating the definition.

## Sources

Where installed bundles came from. `craftsman install <uri>` appends a row here and materializes the bundle's
files under `bundles/<id>/` — `directives/` and `protocols/` inside it, mirroring the top level. `Version` is the
source's commit sha at last sync, when it is a git repository — re-run `craftsman install <uri>` with the same URI
any time to check whether it has moved on.

| Name     | Location        | Kind  | Version |
|----------|-----------------|-------|---------|
| workshop | `.` (this repo) | local | —       |

## Examples

What belongs in a bundle, versus staying at the top level:

- [`gwt-digest`](gwt-digest/bundle.md) — extracting rules section by section is one pipeline: nobody
  wants `extract-rules-batch` without `digest-requirements` to drive it. **Bundle.**
- [`locate-target`](../protocols/locate-target/protocol.md) — used by three different scenarios across two
  bundles (`tdd`, `module-bootstrap`). A part used by many themes is shared, not owned by one. **Fundament.**
- [`prefer-lombok`](../directives/prefer-lombok/directive.md) — a single, standalone preference. Bundling one entry
  alone would just rename it. **Fundament.**

## Bundles

Each bundle has two tables of its own — **Enabled** / **Disabled** — for its members, inside its own `bundle.md`.
This top table only tracks the bundles themselves.

**Enabled**

| No | Id               | Title                                               | Requires     | Path                                                     |
|----|------------------|-----------------------------------------------------|--------------|----------------------------------------------------------|
| 1  | gwt-digest       | Extract Given/When/Then rules from raw requirements | —            | [gwt-digest/bundle.md](gwt-digest/bundle.md)             |
| 2  | testing          | How a test suite is shaped                          | —            | [testing/bundle.md](testing/bundle.md)                   |
| 3  | spec-writing     | Turn accepted use cases into written task specs     | —            | [spec-writing/bundle.md](spec-writing/bundle.md)         |
| 4  | event-storming   | Event storming from a requirements input            | —            | [event-storming/bundle.md](event-storming/bundle.md)     |
| 5  | module-bootstrap | Found a new project or module                       | —            | [module-bootstrap/bundle.md](module-bootstrap/bundle.md) |
| 6  | tdd              | Test-first implementation loop                      | testing      | [tdd/bundle.md](tdd/bundle.md)                           |
| 7  | legacy-code      | Characterization test loop                          | testing, tdd | [legacy-code/bundle.md](legacy-code/bundle.md)           |

**Disabled**

Empty — nothing has been switched off yet.

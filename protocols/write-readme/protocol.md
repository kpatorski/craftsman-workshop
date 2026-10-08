---
id: write-readme
title: Write or update the README
description: >
  Writes the project's README.md from what is actually in the project — build files, configuration, how it starts
  — or brings an existing one in line with the readme directive, and checks that its commands really run.
input: the project — its build files, configuration and templates, scripts, container files — and its README.md, if any
output: README.md written or updated, its commands run where that is safe, confirmed by the developer
uses: [readme]
checkpoint:
  type: ask
  blocking: true
  shows: [full-diff]
  prompt: >
    README <written / updated>: sections <list>. Commands run and working: <list>. Not run: <list, and why —
    e.g. needs a real key>. Placeholders for you to check: <list>. Accept, or change?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Gather the facts from the project itself, never from memory: the build files (toolchain and its version, the
   build/run/test commands), configuration templates and environment variables the code reads, container and
   compose files, scripts. A fact the project does not reveal — where a key comes from, which external service to
   point at — becomes a `<placeholder>` and is named at the checkpoint, never guessed. In a project with several
   modules or build files, this reading may be split between helpers, one per module, as delegated read-only
   preparation (`EXECUTION.md`, same name) — each fact returned with the file and line it comes from.
2. Write the README per [readme](../../directives/readme/directive.md). With an existing README, keep what is right,
   fix what breaks the directive, and remove what does not belong (decision history, personal tools, local paths) —
   say what was removed at the checkpoint.
3. Run every command it contains that is safe to run here — build, tests, start and stop — from the repository root,
   exactly as written. Fix any that fails. A command that cannot be run safely (needs a real secret, deploys,
   touches shared data) is listed at the checkpoint as not run, with the reason.
4. Stop at the checkpoint above before writing the file.

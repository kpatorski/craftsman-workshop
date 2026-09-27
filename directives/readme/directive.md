---
id: readme
title: A README any developer can follow
description: >
  A project's README.md is a short, shared document of facts: what the project is, how to set it up, how to run and
  stop it, and what else a developer needs to work on it — every instruction a command that can be copied and run
  on any machine, nothing about the author's own setup and nothing about how decisions were reached.
applies-when: writing or changing a project's README.md
precedence: >
  the project's existing section names and layout win; the rules on commands, portability, tools and history always
  apply
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must:

- **Structure.** A `#` title (the project's name), then a 2–3 sentence introduction saying what the project is and
  who it is for, then a table of contents when there are more than three sections, then the sections as `##`
  headings.
- **Order.** Sections go in the order a new developer needs them:
  1. setting up — prerequisites, installing, one-time configuration (keys, environment variables, local config
     files);
  2. running and stopping the project;
  3. everything else a developer needs to work on it (tests, useful commands, where to find things).
- **Every instruction is a command.** An instruction that tells the reader to do something gives the exact command
  that does it, in a code block they can copy and run: "copy `x` to `y`" is `cp x y`; "set `A` in `.env`" is the
  full line or command, with a `<placeholder>` for what only the reader knows and one line saying where to get it.
  Prose describing a step without its command is not an instruction.
- **Portable.** Paths are relative to the repository root, never absolute or tied to one machine. Prefer commands
  that behave the same on every operating system — the project's own wrappers and scripts (`./gradlew`, `npm run`,
  `make`), containers. Where a command genuinely differs between systems, give each variant, labelled.
- **Only the tools the project needs.** Name what the project requires to build and run — git, a container runtime
  when the project uses one, the language toolchain with its version — and nothing from one developer's personal
  setup: no version managers (sdkman, nvm, pyenv, asdf, …), no shell aliases, no editor. State the required
  version; how a reader installs it is theirs to choose.
- **Concise.** Only what a developer needs to set up, run, and work on the project. Packaging internals,
  architecture conventions, and design rationale do not belong here — link to where they live, if anywhere.
- **Facts, in the present tense.** No history of how the project got here: no decision logs, no "after discussing
  with the developer we agreed not to…", no changelog entries, no "previously this used…". A README states what is
  true now.
- **Written for everyone on the team.** No "I", no references to the author's machine, session, or conversation.

## Examples

Not an instruction — nothing to copy, and a local path nobody else has:

    Copy the example config from /Users/anna/work/shop/config/example.yml into the config folder and fill in the
    API key. We decided on YAML after discussing it with the team, because TOML was harder to validate.

The same step, as the directive wants it:

    Create the local config and fill in the API key (ask the team lead for a test key):

    ```
    cp config/example.yml config/local.yml
    ```

    ```yaml
    # config/local.yml
    payments:
      api-key: <your test API key>
    ```

A personal tool, versus the fact the reader actually needs:

    Run `sdk use java 21.0.2-tem`, then `./gradlew bootRun`.     ← sdkman is one developer's choice

    Requires Java 21.

    ```
    ./gradlew bootRun
    ```

---
id: simplest-solution
title: The simplest code that does the job, or none at all
description: >
  Before code is written, and when a review reads code a change adds, it goes down a ladder of cheaper options and
  stops at the first that works: no code, code the project already has, the standard library, the framework in use,
  a dependency already in the build, a well-known maintained library, a shorter form. Never at the cost of
  validation, error handling, security or tests.
applies-when: writing production code, or reviewing production code a change adds
precedence: the project's existing conventions decide how; the hard limits never yield
enabled-by-default: true
---

## Schema

Introduces no new fields — see `core.md`.

## Directive

Must — go down the ladder in order and stop at the first rung that holds:

1. **It need not exist.** The requirement is met without it, or nothing calls it.
2. **The project already has it.** A method, a class or a component that does the same — search before writing.
3. **The standard library does it.** For Java: `java.util`, `java.time`, streams, `Objects`, `Optional`.
4. **The framework in use does it.** For Spring: `@Retryable`, `@Scheduled`, `@Transactional`, bean validation.
5. **A dependency already in the build does it.** Lombok, Apache Commons, Guava, Vavr — whatever the build file
   already declares.
6. **A well-known, maintained library does it.** Maintained means a release in the last 12 months and an active
   repository — checked when the session can reach Maven Central or the repository, and said to be unchecked when it
   cannot. It is a new dependency: proposed as one, with its coordinates and version, never added silently.
7. **It can be written shorter and stay as clear.** Fewer branches, one expression instead of a loop.
8. Only then: the minimum that works.

Never simplified away — these hard limits hold on every rung:

- validation of input at a trust boundary
- error handling, and what happens when a call fails
- security: who may call it, what comes from outside, secrets
- a test for logic that branches, loops, parses, or handles money

In a review, a simplification is a finding of category `simplify`. Its comment names the rung, shows the code before
and after, and says what the proposal rests on:

- rungs 4 and 5 — the build file and the line that declares the framework module or the dependency, e.g.
  `pom.xml:42 org.springframework.retry:spring-retry`. Not found in the build → it is rung 6, not 4 or 5.
- rung 6 — in its first sentence that it adds a dependency, then its coordinates, version, and last release date, or
  that the release date is unchecked.

Must not:

- replace code with a library call that behaves differently at the edges (`null`, empty input, time zone, rounding)
  without saying so
- propose a new dependency for one small function that is clearer written by hand
- propose a framework feature or a library without having looked for it in the build file
- shorten code until it is harder to read — shorter only when as clear

[libraries-first](../libraries-first/directive.md) is the utility-method case of rungs 3 to 6.

## Examples

A hand-written retry loop in `AbstractNotifier.retry`, in a Spring project that already has `spring-retry`: rung 4,
`@Retryable(maxAttempts = 3)` on the method that sends. Without `spring-retry` in the build: rung 6, proposed as a new
dependency, `org.springframework.retry:spring-retry` with its version.

Hand-written getters in `CancellationResult`, in a project that builds with Lombok: rung 5, `@Value`.

A new `isBlank(String)` helper in a project that already depends on Apache Commons Lang: rung 5,
`StringUtils.isBlank`.

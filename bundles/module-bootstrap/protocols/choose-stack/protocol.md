---
id: choose-stack
title: Agree the stack
description: >
  Analyse the task's requirements first and propose candidates with reasoning, without consulting enabled stack-preference directives. Only when candidates come out comparable do those preferences break the tie — they never pre-decide the stack. Redesigned from the old version, which started from a fixed default-stack reference; see the `craftsman` plan, decision 5.
input: the module's requirements — expected load, team's language ecosystem, integration constraints, anything the task states or implies
output: an agreed stack for the new module
checkpoint:
  type: ask
  blocking: true
  prompt: >
    From the requirements, I see candidates <A, B, ...> with <reasoning>. <If comparable: enabled preferences favour
    <X> — breaking the tie.> Proposed stack: <list>, each at its latest stable version. Good, or adjust?
---

## Schema

Introduces no new fields — see [core.md](../../../../../craftsman/plugins/craftsman/core.md).

## Protocol

1. Derive candidates from the requirements alone — do not load any `prefer-*` directive yet.
2. If one candidate clearly fits best, propose it with the reasoning, skipping straight to the checkpoint.
3. If candidates are genuinely comparable, only then consult the enabled `prefer-*` directives (e.g.
   [prefer-lombok](../../../../directives/prefer-lombok/directive.md), [prefer-spock](../../../../directives/prefer-spock/directive.md))
   to break the tie.
4. Resolve every entry to its latest stable version before presenting the checkpoint above.

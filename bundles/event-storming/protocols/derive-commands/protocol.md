---
id: derive-commands
title: Derive the command that triggers each event
description: >
  Derives the command that triggers each event — whether it can be rejected and by which rule, whether it needs
  more than one aggregate (and if so, the process that carries it), attached to its aggregate.
input: the current slice's aggregate with its owned events, and the rules attach-event-rules attached to each event
output: >
  one command per event of the current slice, attached to its aggregate, each marked rejectable — with its
  failure outcomes named — or unconditional; plus any process manager a multi-aggregate command forced
uses: [naming, rich-domain, error-handling]
checkpoint:
  type: ask
  blocking: true
  prompt: >
    Commands: <command -> event, on <aggregate>; rejectable: <failure outcomes> / unconditional>. <If any command
    needed more than one aggregate: name it, and the process manager that carries it — trigger event, second
    command, and what happens when the second command is rejected — then ask whether that is the intended process
    or the aggregate boundary is wrong.> Commands right?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. Name the command whose handling produces the event — imperative, present tense, in ubiquitous language
   (`ReserveDesk`, not `DeskReserver`, `handleReservation` or `ReservationProcessor`). See
   [naming](../../../../directives/naming/directive.md).
2. Decide whether the command is rejectable. The criterion is mechanical, and already sitting in the model: a
   command is rejectable when any rule [attach-event-rules](../attach-event-rules/protocol.md) attached to its
   event can be false at the moment it is handled — those preconditions are exactly what the aggregate checks.
   - Rejectable → name the failure outcomes now, one per rule that can fail. They become the spec's acceptance
     criteria instead of being invented at implement time. This is why
     [rich-domain](../../../../directives/rich-domain/directive.md) requires a Result rather than void, and
     [error-handling](../../../../directives/error-handling/directive.md) requires failures as data.
   - Distinguish rejectable (a business rule says no — modelled, returned) from invalid input (a malformed
     request — rejected at the entrypoint or at value-object construction, never a domain outcome).
   - A command with no rule that can be false is unconditional: say so explicitly rather than inventing a failure
     to look thorough.
3. Count the aggregates the command must change. One is the rule (see
   [aggregate-design](../../../../directives/aggregate-design/directive.md)). If it looks like two:
   - First ask whether the boundary is wrong — that is
     [identify-aggregates](../identify-aggregates/protocol.md)' invariant-visibility question, and the honest
     answer is sometimes "merge". Hand it back there rather than re-litigating it here.
   - Otherwise this is a process, not a command: one aggregate changes and emits its event; a process manager
     (a saga) subscribes and issues the second command to the second aggregate. Name the process, the trigger
     event, the second command, and — the part that always gets skipped — what happens when the second command is
     rejected: a compensating command, or an accepted inconsistency with a named reconciliation. Never "it will
     succeed".
   - The process manager is carried forward as a use case of its own for `derive-use-cases` — it is not absorbed
     into either aggregate's use case.
4. A "command" that only reads and changes nothing is not a command — it is a view; hand it to
   [derive-views](../derive-views/protocol.md).
5. Once confirmed, add this slice's commands to `event-model.md`'s `## Commands` section (create it on the first
   slice) — each command with its event, aggregate, rejectable/unconditional marker and failure outcomes, plus any
   process manager named in step 3.

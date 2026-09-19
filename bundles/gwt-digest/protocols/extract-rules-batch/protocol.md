---
id: extract-rules-batch
title: Extract GWT rules for one section
description: >
  Extracts candidate Given/When/Then rules for one section at the domain level — the UI may trigger a business
  process, it is never the content of the rule. Extraction and phrasing only: nothing is confirmed or written
  here. Whether a candidate is a real business rule or an artefact of how the old system happened to be built
  is triage-rules-batch's question, asked against evidence rather than judgement.
input: one section of the input from read-input
output: >
  candidate GWT rules for this section, phrased at the domain level — not yet confirmed, not yet written
  anywhere
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. For one section/story fragment, extract the business rules it implies as Given/When/Then statements.
2. Keep every rule at the domain level. The input is almost always written from the screen's point of view
   ("the user clicks Book"), so this is where extraction slips by default — the UI may *trigger* a business
   process, but it is never the content of the rule.
   - `when` names the actor's intent in the domain ("Employee requests a reservation"), never the mechanics
     ("Employee clicks Book"). The channel — a screen, an endpoint, an import — is context for the section,
     not part of the rule.
   - `given` is domain state. Test it by removal: if dropping the condition does not change the outcome, it was
     never a Given. "Employee is on the booking page" fails this.
   - `then` is an observable domain outcome (`ReservationConfirmed`), not a screen assertion ("a confirmation
     message is displayed").
   - The whole rule must survive a channel swap — the same process driven by a REST call, a CSV import, or an
     admin console. A rule that does not survive it is a UI script, not a business rule.
   - Stop and rephrase on these words: click, button, page, screen, field, form, navigate, tab, dropdown,
     popup, "is displayed". Not banned outright — a rule genuinely about presentation can exist — but never
     carried through unexamined.
3. Name the actor by its domain role (`Employee`, `Member`), never "user" — "user" hides which role the rule
   constrains.
4. A concrete value belongs in a rule only when it drives the rule. Incidental detail carried over from the
   source — a specific password in a rule about account balance — is noise and stays out.
5. Not every sentence is a business rule. Sort order, layout, wording, colour are real requirements but not
   Given/When/Then material: leave them out rather than dressing them up as rules, and name what was left out
   at the checkpoint.
6. One rule per distinct precondition/outcome pair.
7. Hand every candidate from this section to
   [triage-rules-batch](../triage-rules-batch/protocol.md) — nothing here is confirmed or written to
   business-rules.md; that only happens once a candidate has a cited business reason, or the developer has
   resolved one that doesn't.

## Examples

A correctly phrased candidate — domain-level, ready for triage:

    ~~~rule
    section: "Book a desk"
    given: Desk is marked available for the requested day
    when: Employee requests a reservation for that desk and day
    then: ReservationConfirmed
    ~~~

The same rule as it comes out when screen-level prose is taken at face value — every clause fails a different
test above:

    ~~~rule
    given: Employee is on the desk booking page and the desk shows a green "free" badge
    when: Employee clicks Book
    then: A confirmation message is displayed
    ~~~

The `given` describes navigation and a badge instead of domain state; the `when` names the click instead of the
request; the `then` asserts on the screen instead of on the domain. Drive the same process from a REST call and
nothing in it still reads true — which is the channel-swap test. The first block is this same rule extracted
correctly.

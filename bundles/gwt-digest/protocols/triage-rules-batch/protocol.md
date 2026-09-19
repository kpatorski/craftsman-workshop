---
id: triage-rules-batch
title: Cite each candidate's business reason, or park it
description: >
  Decides which candidates from one section actually enter business-rules.md, by looking for evidence rather
  than by judging. The question is never "is this a legacy artefact?" — that is a judgement no reader of the
  text can make reliably. It is "can I quote, from the input, who benefits and why?" A candidate with a quoted
  reason is written; one without is never written silently. Built for inputs that describe an existing system
  (generated documentation, reverse-engineered writeups), where real rules and implementation accidents sit
  side by side in the same paragraph and the accidents are never labelled as such.
input: candidate GWT rules for one section, from extract-rules-batch
output: >
  cited candidates appended to business-rules.md with their reason; uncited ones resolved by the developer —
  promoted, dropped as legacy, or parked in open-questions.md
checkpoint:
  type: ask
  blocking: true
  when: at least one candidate in this batch has no quoted business reason
  prompt: >
    Section <n> <title> — <k> of <n> candidates have no business reason I can quote from the input: <for each:
    the drafted rule, and what is missing>. For each, one of: give me the reason now, confirm it is a legacy
    artefact and drop it, or park it as an open question for the business?
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. For each candidate, search the section for an explicit statement of **who benefits and how** — an actor and
   the harm avoided or the goal served. Quote it, or paraphrase it closely enough that a reader can find it in
   the source. A reason you composed yourself is not a citation; if the text does not say it, it is missing.
2. **A reason that names only a system, a component, a table, or an index is not a citation.** It describes a
   mechanism, not a need the mechanism serves. Push one level further and ask whether the text says who is
   helped by that mechanism, and how. If it does not, the candidate is uncited. Reverse-engineered documents
   almost always phrase things this way ("the system maintains…", "the application updates…"), so this is the
   single most common shape to catch.
3. This heuristic does not catch everything — a legacy artefact written up with a plausible-sounding business
   reason attached will pass. Say so rather than implying the pass is a guarantee: what a citation proves is
   that a reason exists in the input, not that the reason is true.
4. **When it is unclear whether a reason really is a citation, treat the candidate as uncited.** A wrong
   "uncited" costs one question; a wrong "business rule" costs building something nobody needs. The costs are
   not symmetric, so neither is the default.
5. **Append every cited candidate to business-rules.md in the same turn**, carrying its `reason:` so a
   downstream reader can check it instead of trusting it. Create the file (a one-line header naming the source)
   on the first such candidate; append on every batch after. Never defer a write to the end of the run — a
   confirmed rule that exists only in the session file is invisible to the developer for the whole run.
6. **No uncited candidate is ever written to business-rules.md without an answer.** State the batch's outcome in
   one line either way (how many were cited and appended, how many are flagged); stop only when something is
   flagged.
7. Record the developer's resolution in the same turn:
   - **reason supplied** — the candidate becomes a cited rule, written as in step 5, with the supplied reason
     as its `reason:`
   - **confirmed legacy** — dropped, with the reason noted in the session's checkpoint log so a later run does
     not re-ask the same question
   - **parked** — appended to `open-questions.md`, in the block form below

`open-questions.md` follows the same convention as `business-rules.md`: the root of the target project, written
incrementally, one block per parked candidate. For a developer who inherited a system nobody understands, this
file is usually the more valuable of the two — it is the list of questions for the business that nobody has.

## Examples

Cited. The source says who is hurt and how, so the reason is quotable and the rule is written without stopping:

> An employee must not be able to book a desk that is already taken for that day — otherwise two people turn up
> at the same desk.

    ~~~rule
    id: reservation-rejected-when-desk-taken
    section: "Book a desk"
    given: Desk is already reserved for the requested day
    when: Employee requests a reservation for that desk and day
    then: ReservationRejected
    reason: "otherwise two people turn up at the same desk"
    ~~~

Uncited, obvious case. The candidate is phrased perfectly — domain-level, one precondition, one outcome, no UI
anywhere — and still has nothing behind it:

> The system maintains a search index, refreshed after every record change, so that searches return in an
> acceptable time.

    ~~~question
    id: search-index-refresh
    section: "Search"
    candidate: given a record has changed / when the change is committed / then the search index is refreshed
    missing: >
      The only reason in the text is the index itself. Nobody is named as benefiting, and "acceptable time" is
      not quantified. A new system may need no index at all — what it needs is whatever search latency the
      business actually requires.
    ~~~

Uncited, subtle case — the one the heuristic exists for. This reads like a retention rule, and a careless pass
would write it down as one:

> Records older than 30 days are moved to the archive so the main table does not grow indefinitely.

    ~~~question
    id: archive-after-30-days
    section: "Data lifecycle"
    candidate: given a record is older than 30 days / when the archival runs / then the record is archived
    missing: >
      The reason names a table, not a person. Nothing says the business requires 30-day retention, or any
      retention at all — the number may exist only because one table grew too large on the old hardware.
    ~~~

The difference between the first block and the other two is not how well the rule is phrased. All three are
phrased correctly. It is whether the input says who needs it.

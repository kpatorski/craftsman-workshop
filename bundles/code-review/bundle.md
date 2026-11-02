---
id: code-review
title: Review a pull request
description: >
  Reviews a pull request, or the difference between two branches, the way an engineer who knows the domain would:
  first what the change is for and how it is shaped, then the code, use case by use case, against the enabled
  directives — and proposes comments the developer edits, picks and sends.
---

## Schema

No fields of its own — see `core.md`.

## Bundle

Understanding comes before judging. The review reads the PR's description and the requirements it links, finds the
use cases the change adds or changes, how each one runs and which boundaries its calls cross, and reads the tests for
the business rules — all of it confirmed with the developer before a single line of code is judged. Only then does it
walk the code, use case by use case, from the entry point down: module, class, method, parameters.

What it produces is a set of findings, never comments sent on its own: the developer edits, deletes or marks each
one, and decides when to send. The directives here say what a finding is and how its comment reads; what the code
itself is checked against are the enabled directives of the workshop, the same ones `implement` writes code by.

## Protocols

**Enabled**

| No | Id                                                                 | Title                                             |
|----|--------------------------------------------------------------------|---------------------------------------------------|
| 1  | [open-review](protocols/open-review/protocol.md)                   | Open a review                                     |
| 2  | [read-pr-scope](protocols/read-pr-scope/protocol.md)               | Read what the PR is for                           |
| 3  | [map-change-structure](protocols/map-change-structure/protocol.md) | Map the structure of the change                   |
| 4  | [read-test-rules](protocols/read-test-rules/protocol.md)           | Read the business rules from the tests            |
| 5  | [triage-explanations](protocols/triage-explanations/protocol.md)   | Explain the places that are hard to follow        |
| 6  | [review-use-cases](protocols/review-use-cases/protocol.md)         | Review the code use case by use case              |
| 7  | [review-use-case](protocols/review-use-case/protocol.md)           | Review one use case, from its entry point down    |
| 8  | [deduplicate-findings](protocols/deduplicate-findings/protocol.md) | Make one finding of each problem                  |
| 9  | [serve-page](protocols/serve-page/protocol.md)                     | Answer the review page until the review is closed |
| 10 | [refresh-review](protocols/refresh-review/protocol.md)             | Bring the review up to date with the PR           |

**Disabled**

Empty — nothing has been switched off yet.

## Directives

**Enabled**

| No | Id                                                       | Title                                                                    |
|----|----------------------------------------------------------|--------------------------------------------------------------------------|
| 1  | [review-comment](directives/review-comment/directive.md) | A review comment names the problem, its consequence, and a fix           |
| 2  | [review-posture](directives/review-posture/directive.md) | An existing convention changes a finding's kind, never whether it exists |
| 3  | [engineer-prose](directives/engineer-prose/directive.md) | Review texts read like one engineer briefing another                     |

**Disabled**

Empty — nothing has been switched off yet.

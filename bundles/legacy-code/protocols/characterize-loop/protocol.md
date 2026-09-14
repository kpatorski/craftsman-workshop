---
id: characterize-loop
title: Characterization test loop
description: >
  Adds tests to code that already exists. No production code is written and nothing is designed — each test captures what the code does now.
input: existing, working, untested code
output: passing characterization tests, committed on their own
steps: [decide-test-level, scaffold-suite, enumerate-cases-from-code, characterize-cycle, finish-characterize, commit-tests]
done-when: every observed behaviour path has a passing test and they are committed on their own
---

## Schema

Introduces no new fields — see `core.md`.

## Protocol

1. [decide-test-level](../../../tdd/protocols/decide-test-level/protocol.md)
2. [scaffold-suite](../../../tdd/protocols/scaffold-suite/protocol.md)
3. [enumerate-cases-from-code](../enumerate-cases-from-code/protocol.md)
4. [characterize-cycle](../characterize-cycle/protocol.md)
5. [finish-characterize](../finish-characterize/protocol.md)
6. [commit-tests](../commit-tests/protocol.md)

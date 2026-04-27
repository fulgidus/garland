---
name: tdd
description: Apply Test-Driven Development discipline. Use when writing any new function, module, or feature from scratch. Do NOT trigger when writing config files, database migrations, purely declarative markup, or when asked only to read/analyse existing code.
---

# TDD

## Rules

1. Write a failing test before writing any production code — the test defines the interface.
2. Write the minimum code to make the test pass. No more.
3. Refactor — both the new code and the existing code — before moving to the next test. Skipping this step turns TDD into tested spaghetti.
4. Start each feature with a written list of test cases. Sequence them to drive toward the salient design decisions as quickly as possible.
5. Use the five test double types precisely: Dummy (fill parameter lists), Fake (working shortcut), Stub (canned answers), Spy (stub that records), Mock (pre-programmed expectations). Never use "mock" as a catch-all.
6. Default to state verification (assert the outcome). Use behaviour verification (assert the calls) only when the outcome is unobservable.
7. Prefer real collaborators. Only double what is genuinely awkward: external I/O, email, clocks, randomness.
8. Complement unit tests with at least one coarse-grained acceptance test across the full flow.

## Anti-patterns

- Do not write tests after the code is working — they will confirm what you already know, not shape the design.
- Do not skip the Refactor step. Green + no-refactor = design debt with a green light.
- Do not write mockist tests that encode the call structure of a method when you only care about the result — they break on legitimate refactors.
- Do not mock collaborators that are easy to use for real.

## Refs

- [[wiki/beliefs/testing]]
- [[wiki/sources/tdd-fowler]]
- [[wiki/sources/mocks-arent-stubs]]

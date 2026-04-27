---
title: "Testing"
parent: "Beliefs"
grand_parent: "Wiki"
---

# Testing

## Position

Tests are a design tool first, a safety net second. Writing tests before code forces interface design before implementation — the separation most developers skip. The discipline only works if the full Red-Green-Refactor loop is completed; stopping at Green produces tested spaghetti. Test doubles are a precise vocabulary, not interchangeable synonyms: choosing the wrong double produces tests that verify the wrong thing or break during legitimate refactors.

## Rules

- DO: write the test before the code; treat it as a design act that defines the interface. [[tdd-fowler]]
- DO: complete all three steps — Red, Green, Refactor — every cycle. [[tdd-fowler]]
- DO: start a feature by writing a list of test cases first; sequence them to reach salient design decisions quickly. [[tdd-fowler]]
- DO: learn the five test double types (Dummy, Fake, Stub, Spy, Mock) and use them precisely. [[mocks-arent-stubs]]
- DO: use state verification (assert the outcome) by default; use behaviour verification (assert the calls) only when outcome is unobservable. [[mocks-arent-stubs]]
- DO: complement unit tests with coarse-grained acceptance tests across the whole system. [[mocks-arent-stubs]]
- DON'T: skip the Refactor step; untouched passing code accumulates design debt faster than no tests at all. [[tdd-fowler]]
- DON'T: use "mock" as a catch-all for any test double. [[mocks-arent-stubs]]
- DON'T: mock collaborators that are not genuinely awkward (external I/O, email, time); prefer real objects. [[mocks-arent-stubs]]
- DON'T: write mockist tests that encode call structure when you only care about the result — they break on refactors. [[mocks-arent-stubs]]

## Open questions

- At what granularity should clusters of collaborators be tested together without mocking?
- When does the fixture setup cost of classical TDD justify switching to mockist style?

## Conflicts

> CONFLICT: Classical TDD ([[mocks-arent-stubs]]) says prefer real objects and only double awkward collaborators. Mockist TDD ([[mocks-arent-stubs]]) says always mock collaborators for isolation.
> Resolution: Both are coherent; Fowler is a classicist. Default to classical; use mockist only when isolation genuinely matters more than coupling risk.

## Sources

- [[tdd-fowler]]
- [[mocks-arent-stubs]]

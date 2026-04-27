---
clipped: 2026-04-27
url: https://martinfowler.com/articles/mocksArentStubs.html
raw: ../../raw/mocks-arent-stubs.md
---

# Mocks Aren't Stubs

## Author / context

Martin Fowler, martinfowler.com, January 2007 (revised). Definitive article distinguishing mock objects from other test doubles, and mapping the classical vs. mockist TDD divide.

## Summary

The word "mock" is used loosely to mean any fake object in a test, but Fowler (following Meszaros) establishes five precise categories of test double: Dummy, Fake, Stub, Spy, Mock. Only Mocks enforce behaviour verification — asserting which calls were made on collaborators. Everything else uses state verification — asserting what the object looks like afterwards. This distinction maps onto two philosophies: Classical TDD (use real objects where possible, double only awkward collaborators) and Mockist TDD (always double every collaborator). Each has distinct tradeoffs around coupling, isolation, and design feedback.

## Key precepts

- Learn the five test double types; never use "mock" as a catch-all.
- Mocks verify behaviour (calls made); stubs verify state (end result). Use the right tool for the question you're asking.
- Classical TDD: prefer real objects; only double what's genuinely awkward (e.g. external services, email).
- Mockist TDD: always mock collaborators; gives finer isolation but couples tests to implementation.
- Mockist tests break during refactoring more often because they encode call structure, not outcome.
- Every test suite — classical or mockist — must be complemented with coarse-grained acceptance tests.

## Verbatim anchors

> "mock objects are but one form of special case test object, one that enables a different style of testing"

> "Mocks are what we are talking about here: objects pre-programmed with expectations which form a specification of the calls they are expected to receive."

> "Coupling to the implementation also interferes with refactoring, since implementation changes are much more likely to break tests than with classic testing."

## Topics

- [[../beliefs/testing]]

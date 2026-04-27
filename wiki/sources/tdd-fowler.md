---
title: "TDD (Fowler)"
parent: "Sources"
grand_parent: "Wiki"
---

# Test Driven Development

## Author / context

Martin Fowler, martinfowler.com, originally 2005, updated December 2023. Canonical bliki entry summarising Kent Beck's TDD technique from Extreme Programming.

## Summary

TDD is a development rhythm, not a testing strategy. You write a failing test, write just enough code to pass it, then refactor both. The discipline forces you to design interfaces before implementations — a separation most developers find difficult to achieve when writing code first. The refactor step is non-negotiable: skipping it turns TDD into tested spaghetti.

## Key precepts

- Write the test before the code; the test is a design act, not a verification act.
- Follow Red-Green-Refactor strictly; omitting Refactor defeats the practice.
- Start each feature by writing a list of test cases first; sequence them to drive toward salient design decisions.
- Writing tests first forces interface/implementation separation, which is a core design skill.

## Verbatim anchors

> "The most common way that I hear to screw up TDD is neglecting the third step. Refactoring the code to keep it clean is a key part of the process, otherwise we just end up with a messy aggregation of code fragments."

> "thinking about the test first forces us to think about the interface to the code first. This focus on interface and how you use a class helps us separate interface from implementation"

## Topics

- [[../beliefs/testing]]

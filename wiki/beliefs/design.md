---
title: "Design"
parent: "Beliefs"
grand_parent: "Wiki"
---

# Design

## Position

Good software design is not subjective. Beck's four rules provide a concrete, priority-ordered definition that is evaluable in the present, not in hindsight. A design is good if — in order — it passes the tests, reveals the author's intention to the next reader, contains no duplication, and has the fewest elements that satisfy the first three. Anything else is speculation, and speculation adds complexity that makes systems less flexible, not more.

## Rules

- DO: apply Beck's rules in priority order: passes tests → reveals intention → no duplication → fewest elements. [[beck-design-rules]]
- DO: treat "reveals intention" as a communication obligation to the next reader, not an aesthetic preference. [[beck-design-rules]]
- DO: eliminate duplication as a design driver; the exercise of removing it tends to surface the right abstraction. [[beck-design-rules]]
- DO: delete any element (class, method, abstraction) that does not serve the first three rules. [[beck-design-rules]]
- DON'T: add abstractions speculatively for future flexibility; extra complexity makes systems harder to change. [[beck-design-rules]]
- DON'T: treat design quality as a matter of taste; evaluate it against concrete criteria now. [[beck-design-rules]]
- DON'T: resolve the tension between "no duplication" and "reveals intention" by adding duplication — find the abstraction that satisfies both. [[beck-design-rules]]
- DO: make invalid states unrepresentable — model the type system so that values that should not exist cannot be constructed. [[everything-should-be-typed]]

## Open questions

- How do Beck's rules interact with domain-driven design, where duplication across bounded contexts is sometimes intentional?

## Conflicts

_(none)_

## Sources

- [[beck-design-rules]]
- [[everything-should-be-typed]]

---
clipped: 2026-04-27
url: https://martinfowler.com/bliki/BeckDesignRules.html
raw: ../../raw/beck-design-rules.md
---

# Beck Design Rules

## Author / context

Martin Fowler documenting Kent Beck's four rules of simple design, martinfowler.com, March 2015. Beck formulated the rules during the development of Extreme Programming in the late 1990s.

## Summary

Beck's four rules give a concrete, priority-ordered definition of "good design" — a replacement for vague taste-based judgements. The rules are: (1) passes the tests, (2) reveals intention, (3) no duplication, (4) fewest elements. Priority order matters: passing tests is non-negotiable; readability beats DRY when they conflict; and anything that doesn't serve the first three rules should be deleted. The rules are language-agnostic and hold across paradigms.

## Key precepts

- Good design is not subjective; these four rules are evaluable right now, not post-hoc.
- Priority order is the whole point: passes tests > reveals intention > no duplication > fewest elements.
- "Reveals intention" means code communicates the author's purpose to the next reader.
- "No duplication" = Once and Only Once; duplication to increase clarity is papering over a design problem.
- "Fewest elements" = delete speculative abstractions; extra complexity added for future flexibility usually makes things less flexible in practice.

## Verbatim anchors

> "Passes the tests / Reveals intention / No duplication / Fewest elements"

> "At the time there was a lot of 'design is subjective', 'design is a matter of taste' bullshit going around. I disagreed. There are better and worse designs." — Kent Beck

> "anything that doesn't serve the three prior rules should be removed"

## Topics

- [[../beliefs/design]]

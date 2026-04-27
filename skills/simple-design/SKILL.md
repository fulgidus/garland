---
name: simple-design
description: Apply Beck's four rules of simple design. Use during refactoring, code review, or when evaluating whether to add, keep, or delete an abstraction. Do NOT trigger during initial greenfield spiking where the only goal is getting something to run.
---

# Simple Design

## Rules

1. Apply the four rules in strict priority order:
   1. **Passes the tests** — non-negotiable. Nothing else matters if this fails.
   2. **Reveals intention** — code communicates its purpose to the next reader.
   3. **No duplication** — Once and Only Once. Eliminating duplication surfaces the right abstraction.
   4. **Fewest elements** — delete anything (class, method, abstraction) that does not serve rules 1–3.
2. Treat "reveals intention" as a communication obligation, not an aesthetic preference.
3. Use the exercise of eliminating duplication as a design driver — it tends to produce the correct abstraction naturally.
4. When rules 2 and 3 appear to conflict, look for the abstraction that satisfies both rather than resolving it with added duplication.
5. Make invalid states unrepresentable: model types and data structures so that values that should not exist cannot be constructed.

## Anti-patterns

- Do not add abstractions speculatively for future flexibility — extra complexity makes systems harder to change, not easier.
- Do not treat design quality as a matter of taste; evaluate it against these four criteria now, not in hindsight.
- Do not add duplication to increase readability as a first move — it papers over a missing abstraction.

## Refs

- [[wiki/beliefs/design]]
- [[wiki/sources/beck-design-rules]]
- [[wiki/sources/everything-should-be-typed]]

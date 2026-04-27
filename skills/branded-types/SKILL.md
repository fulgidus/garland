---
name: branded-types
description: Apply TypeScript branded domain types and Zod boundary validation. Use when writing or reviewing TypeScript code that passes domain-meaningful primitives (IDs, money amounts, units, user input) as function arguments or object fields. Do NOT trigger for generic utility types, pure infrastructure plumbing, or non-TypeScript code.
---

# Branded Types

## Rules

1. Define a branded type for every domain-meaningful primitive: IDs, money, units, sanitised strings.
2. Use `Brand<T, B extends string> = T & { readonly [__brand]: B }` with `declare const __brand: unique symbol` as the canonical helper — one definition per codebase.
3. Brand individual values, not object containers. A branded wrapper on a struct/interface still allows semantically wrong values in its fields.
4. Validate and brand exactly once at the system boundary (API response, form input, URL param, WebSocket message). Use Zod `.brand()` as the default: one schema delivers runtime validation + compile-time branding in a single `parse()`.
5. Trust branded types everywhere inside the boundary. No inner function re-validates what the constructor already guaranteed.
6. Model unsafe conversions explicitly: `RawUserInput` must be converted to `SanitizedHtml` before rendering — enforced by the type, not by convention.

## Anti-patterns

- Do not use `string` or `number` directly as parameters when the argument has a specific domain role.
- Do not brand the container object (`type BrandedPayout = Params & { __brand: "X" }`) and consider the job done.
- Do not re-validate branded values inside service or repository layers.
- Do not use string-literal intersection branding (`type X = string & { __brand: "X" }`) when `unique symbol` is available — the latter is unassignable by accident.

## Refs

- [[wiki/beliefs/typing]]
- [[wiki/sources/everything-should-be-typed]]

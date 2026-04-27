---
title: "Typing"
parent: "Beliefs"
grand_parent: "Wiki"
topic: typing
updated: 2026-04-27
---

# Typing

## Position

Scalar types (`string`, `number`, `boolean`) describe the shape of data, not its domain meaning. A structural type system cannot distinguish a `ShopId` from a `CustomerId` if both are `string` — and every real codebase has this bug somewhere. The fix is branded domain types: wrap every meaningful primitive at definition time, validate it once at the system boundary, and let the compiler enforce correctness everywhere else. The cost is one to four lines per type. The alternative is trusting every developer in every PR to get it right.

## Rules

- DO: define a branded type for every domain-meaningful primitive — IDs, money amounts, units, sanitised strings. [[everything-should-be-typed]]
- DO: use `Brand<T, B extends string> = T & { readonly [__brand]: B }` with `unique symbol` as the canonical helper. [[everything-should-be-typed]]
- DO: brand individual *values*, not object containers — a branded wrapper around `OrderPayoutParams` still lets you fill its fields with semantically wrong values. [[everything-should-be-typed]]
- DO: validate and brand at the system boundary (API response, form input, URL param, WebSocket message) exactly once. [[everything-should-be-typed]]
- DO: trust branded types everywhere inside the boundary — no function should re-validate what the constructor already guaranteed. [[everything-should-be-typed]]
- DO: use Zod `.brand()` as the default FE validation strategy — one schema delivers runtime validation + compile-time branding in a single `parse()` call. [[everything-should-be-typed]]
- DO: use a `RawUserInput` → `SanitizedHtml` conversion type to enforce injection safety at the compiler level. [[everything-should-be-typed]]
- DON'T: use `string` or `number` directly as function parameters when the argument has a specific domain role. [[everything-should-be-typed]]
- DON'T: brand the container object and consider the job done — the brand must live on each value. [[everything-should-be-typed]]
- DON'T: re-validate branded values inside service/repository layers — that is the boundary's job. [[everything-should-be-typed]]

## Open questions

- At what granularity should branding stop? (e.g. should `EmailLocalPart` and `EmailDomain` be separate types from `Email`?)
- How does Zod `.brand()` interact with tRPC and server-side type sharing across a full-stack TypeScript monorepo?

## Conflicts

_(none)_

## Sources

- [[everything-should-be-typed]]

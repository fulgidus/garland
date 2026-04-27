---
title: "Everything Should Be Typed"
parent: "Sources"
grand_parent: "Wiki"
clipped: 2026-04-27
url: https://sot.dev/everything-should-be-typed.html
raw: ../../raw/everything-should-be-typed.md
---

# Everything Should Be Typed: Scalar Types Are Not Enough

## Author / context

Samuel (original article, sot.dev, 13 April 2026) + Alessio Giulio Corsi (FE rendition, TypeScript/Zod focus, 14 April 2026). Born from a real production bug: a seller received ₦350 instead of ₦54,000 because positional arguments of the same scalar type were silently swapped.

## Summary

Scalar types (`string`, `number`) describe the *shape* of data, not its *meaning*. A structural type system like TypeScript's cannot distinguish a `ShopId` from a `CustomerId` if both are `string` — so swapping them is a silent, compile-passing, test-passing bug. The solution is to wrap every meaningful value in a domain-specific branded type, validate it once at the system boundary, and let the compiler carry that guarantee everywhere. Alessio's FE rendition adds the `Brand<T,B>` helper with `unique symbol`, the Zod `.brand()` pattern as the practical frontend default, and a Manual/Zod/Ajv comparison.

## Key precepts

- Scalar types (`string`, `number`) describe shape, not meaning — two values with the same shape are structurally interchangeable, even when domain-semantically incompatible.
- Named object fields prevent positional swaps but not semantic ones; you need branded *values*, not branded *containers*.
- Use `Brand<T, B extends string> = T & { readonly [__brand]: B }` with a `unique symbol` as the canonical TypeScript branded type helper.
- Validate at the boundary (API, form, URL, WebSocket); once a branded type exists, trust it everywhere inside — no re-validation.
- Zod `.brand()` is the natural FE default: one schema delivers runtime validation + compile-time branding in a single `parse()` call.
- Make invalid states unrepresentable: if a `ShopId` exists in the system, it is valid by construction.
- A `RawUserInput` type that must be explicitly converted to `SanitizedHtml` before rendering enforces injection safety at the type level.

## Verbatim anchors

> "The compiler checks the *shape* of the data, not the *meaning*."

> "You need to brand **each individual value**, not the container."

> "Scalar types describe **what a value looks like**. Domain types describe **what a value means**. The distance between the two is where bugs live."

> "That is not engineering. That is hope."

## Topics

- [[typing]]
- [[design]]

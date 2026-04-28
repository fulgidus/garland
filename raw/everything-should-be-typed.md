---
clipped: 2026-04-27
url: https://sot.dev/everything-should-be-typed.html
author: Samuel Onoja (original) · Alessio Giulio Corsi (FE rendition, 14/04/2026)
raw: ../../raw/everything-should-be-typed.md
---

# Everything Should Be Typed: Scalar Types Are Not Enough

> Original: [sot.dev/everything-should-be-typed](https://sot.dev/everything-should-be-typed.html) by Samuel, 13 April 2026.  
> This file merges the original article with Alessio's frontend-centred rendition ("I tipi scalari non bastano: la prospettiva del frontend").  
> Sections marked **[AC]** are Alessio's additions or FE-specific framings.  

---

## The Positional Parameter Problem

Consider a function that processes a seller payout:

```ts
function processOrderPayout(
  shopId: string,
  customerId: string,
  orderId: string,
  amount: number,
  platformFee: number,
  txFee: number,
  netAmount: number,
) { /* ... */ }
```

Seven parameters. Three `string`. Four `number`.
The compiler is happy. The domain is crying.

A caller writes this:

```ts
processOrderPayout(
  customerId,   // 👈 was shopId
  shopId,       // 👈 was customerId
  orderId,
  netAmount,    // 👈 was amount
  txFee,        // 👈 was platformFee
  platformFee,  // 👈 was txFee
  amount,       // 👈 was netAmount
);
```

`tsc` doesn't complain. Tests pass. The seller receives ₦350 instead of ₦54,000.

> **The compiler checks the *shape* of the data, not the *meaning*.**

TypeScript uses a *structural* type system: two values with the same shape are interchangeable.

| What `tsc` sees | What we meant         |
| --------------- | --------------------- |
| `string`        | Shop ID               |
| `string`        | Customer ID           |
| `number`        | Gross amount in cents |
| `number`        | Platform fee in cents |

Same type → no error → silent bug.

---

## "Just Use an Object." Better, But Not Enough.

```ts
interface OrderPayoutParams {
  shopId: string;
  customerId: string;
  orderId: string;
  amount: number;
  platformFee: number;
  txFee: number;
  netAmount: number;
}

function processOrderPayout(params: OrderPayoutParams) { /* ... */ }
```

Named fields eliminate positional confusion. ✅

But the problem that remains:

```ts
const params: OrderPayoutParams = {
  shopId: customerId,   // ⚠️ string → string, no error
  customerId: shopId,   // ⚠️ same
  orderId,
  amount: netAmount,    // ⚠️ number → number, no error
  platformFee: txFee,
  txFee: platformFee,
  netAmount: amount,
};
```

The object gives us **nominal assignment**, not **semantic correctness**.
Fields accept *any* `string` or `number`, not only the ones with the right meaning.

---

## **[AC]** Why Branded Objects Aren't Enough Either

A common intermediate step is to brand the *container*:

```ts
type BrandedPayout = OrderPayoutParams & { __brand: "OrderPayout" };

function processOrderPayout(params: BrandedPayout) { /* ... */ }
```

This prevents passing an arbitrary object as `BrandedPayout` — but it **does not** prevent
filling the fields with swapped values.
The brand is on the wrapper, not on the content.

> You need to brand **each individual value**, not the container.

---

## The Core Problem: Primitives Erase Meaning

Bugs that scalar types will never catch:

- **User ID where an Order ID was expected** — both `string`, wrong table, wrong record.
- **Mixed units** — metres vs km, cents vs euros, seconds vs minutes. All `number`.
- **Unsanitised input** — raw user string straight into a SQL query or HTML template. `string` is `string`. Injection guaranteed.
- **Latitude and longitude swapped** — both `number`. The map renders on the wrong continent.

All compile. All pass tests. All have caused production incidents.

---

## The Solution: Make Invalid States Unrepresentable

### Branded Types in TypeScript

```ts
type ShopId      = string & { readonly __brand: "ShopId" };
type CustomerId  = string & { readonly __brand: "CustomerId" };
type OrderId     = string & { readonly __brand: "OrderId" };
type Amount      = number & { readonly __brand: "Amount" };
type PlatformFee = number & { readonly __brand: "PlatformFee" };
type TxFee       = number & { readonly __brand: "TxFee" };
type NetAmount   = number & { readonly __brand: "NetAmount" };
```

`__brand` is a *phantom property*: it exists only at compile-time, zero runtime overhead.

Now the interface enforces meaning:

```ts
interface OrderPayoutParams {
  shopId: ShopId;
  customerId: CustomerId;
  orderId: OrderId;
  amount: Amount;
  platformFee: PlatformFee;
  txFee: TxFee;
  netAmount: NetAmount;
}

const params: OrderPayoutParams = {
  shopId: customerId,
  //      ~~~~~~~~~~  ❌ Type 'CustomerId' is not assignable to type 'ShopId'
  amount: netAmount,
  //      ~~~~~~~~~  ❌ Type 'NetAmount' is not assignable to type 'Amount'
};
```

The compiler refuses. Not because the *shape* is wrong, but because the *meaning* is wrong.

---

### **[AC]** Generic Helper with `unique symbol`

```ts
declare const __brand: unique symbol;

type Brand<T, B extends string> = T & { readonly [__brand]: B };

// One line per type
type ShopId     = Brand<string, "ShopId">;
type CustomerId = Brand<string, "CustomerId">;
type Amount     = Brand<number, "Amount">;
type NetAmount  = Brand<number, "NetAmount">;
```

`unique symbol` guarantees the brand is never accidentally assignable.

---

## Living with Branded Types: Creating Values

A `Brand<string, "ShopId">` can't be assigned from a plain `string`.
You need a **constructor** — the entry point where you decide the value is valid.

```ts
// Minimal version — explicit cast
function shopId(raw: string): ShopId {
  return raw as ShopId;
}
```

This works but validates nothing. We can do better.

### Manual Validation

```ts
class InvalidShopId extends Error {
  readonly name = "InvalidShopId" as const;
}

function shopId(raw: string): ShopId {
  if (raw === "")
    throw new InvalidShopId("Shop ID cannot be empty");
  if (!raw.startsWith("shop_"))
    throw new InvalidShopId("Shop ID must start with 'shop_'");
  return raw as ShopId;
}
```

✅ Zero dependencies.
✅ Full control over error messages.
⚠️ Scales poorly — repetitive boilerplate as types multiply.

---

### **[AC]** Validation with Zod

Zod has **native support** for `.brand()` — branded types come out of the parser ready to use:

```ts
import { z } from "zod";

const ShopIdSchema = z
  .string()
  .min(1, "Shop ID cannot be empty")
  .startsWith("shop_", "Shop ID must start with 'shop_'")
  .brand("ShopId");

type ShopId = z.infer<typeof ShopIdSchema>;
//   ^? string & { __brand: "ShopId" }

const id  = ShopIdSchema.parse("shop_abc123"); // ShopId ✅
const bad = ShopIdSchema.parse("usr_999");     // 💥 ZodError
```

Full pattern — one schema, one `parse()`, entire payload validated **and** branded:

```ts
const AmountSchema = z
  .number()
  .int("Amount must be an integer (cents)")
  .nonnegative("Amount cannot be negative")
  .brand("Amount");

const OrderPayoutParamsSchema = z.object({
  shopId:      ShopIdSchema,
  customerId:  CustomerIdSchema,
  orderId:     OrderIdSchema,
  amount:      AmountSchema,
  platformFee: PlatformFeeSchema,
  txFee:       TxFeeSchema,
  netAmount:   NetAmountSchema,
});

type OrderPayoutParams = z.infer<typeof OrderPayoutParamsSchema>;
```

---

### **[AC]** Manual vs Zod vs Ajv

| Criterion        | Manual   | Zod             | Ajv (JSON Schema) |
| ---------------- | -------- | --------------- | ----------------- |
| Bundle size      | 0 kB     | ~14 kB (min+gz) | ~30 kB (min+gz)   |
| Native branded   | DIY      | `.brand()` ✅    | no, manual cast   |
| Type inference   | manual   | `z.infer` ✅     | no (codegen)      |
| Runtime validate | if/throw | `.parse()` ✅    | `validate()` ✅    |
| Schema compose   | fragile  | excellent       | `$ref` (verbose)  |
| FE ecosystem     | anything | RHF, tRPC, Hono | Express           |

**Recommendation:** Zod is the natural default for TypeScript frontend projects.
Ajv makes sense when you're starting from existing JSON Schema (e.g. OpenAPI).

---

## Validate at the Boundary, Trust Inside

```
┌──────────────────────────────────────────────────┐
│  API / Form / URL params / WebSocket  ← boundary │
│                                                  │
│  ShopIdSchema.parse(raw) ← validate + brand      │
│         │                                        │
│         ▼                                        │
│  ShopId  ← valid from here on, by construction   │
│         │                                        │
│  service layer → repository → event bus          │
│  no re-validation needed                         │
└──────────────────────────────────────────────────┘
```

Build the type **once** at the boundary.
The type system carries the guarantee all the way through.

---

## What You Actually Gain

- **Self-documenting code** — `fn(shopId: ShopId)` needs no JSDoc to explain what that parameter is.
- **Safe refactoring** — rename a type and `tsc` shows every call site that uses it.
- **Validation at the boundary** — if a `ShopId` exists, it *is* valid. By construction. No inner function needs to re-check.
- **Grep-ability** — search `ShopId` and find every creation, pass, and transformation.
- **Security** — a `RawUserInput` type that must be explicitly converted to `SanitizedHtml` before rendering? Injection prevention enforced by the compiler, not by code review discipline.

---

## The Cost Is Lower Than You Think

A branded type is **one line**.
A Zod schema is **three or four lines**.
The compiler enforces them **forever**.

The alternative? Trusting that every developer on the team, across every PR, in every 2am hotfix, correctly associates anonymous strings with their intended purpose.

> That is not engineering. That is hope.

---

## Summary

| Level                 | What it prevents               |
| --------------------- | ------------------------------ |
| Positional parameters | Nothing                        |
| Object with fields    | Positional swaps               |
| Branded types         | Semantic swaps at compile-time |
| Branded + validation  | Invalid data at runtime        |

Scalar types describe **what a value looks like**.
Domain types describe **what a value means**.

The distance between the two is where bugs live.

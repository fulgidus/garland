---
name: coding-best-practices
description: General software engineering best practices for writing clean, maintainable, and robust code. Use when writing new code, reviewing existing code, or refactoring. Covers naming conventions, error handling, testing, and code organization principles.
license: MIT
metadata:
  author: fulgidus
  version: "1.0.0"
---

# Coding Best Practices

A curated set of software engineering principles for writing clean, maintainable, and robust code.

## When to Apply

Reference these guidelines when:
- Writing new features or modules
- Reviewing or refactoring existing code
- Designing APIs or data structures
- Debugging and fixing issues

## 1. Naming & Readability

- Use intention-revealing names: prefer `getUserById` over `getU`
- Avoid abbreviations unless universally accepted (e.g., `id`, `url`, `html`)
- Name booleans as questions: `isLoading`, `hasError`, `canSubmit`
- Functions should describe actions: `calculateTotal`, `sendEmail`, `parseConfig`
- Constants in `UPPER_SNAKE_CASE`; classes/types in `PascalCase`; variables/functions in `camelCase`
- Keep names consistent within a codebase (don't mix `fetch`/`get`/`retrieve` for the same concept)

## 2. Functions & Methods

- Follow the Single Responsibility Principle: each function does one thing
- Keep functions short (ideally under 20–30 lines); extract helpers if longer
- Limit parameters to 3 or fewer; group related args into an object
- Return early to reduce nesting (`if (invalid) return error` before main logic)
- Prefer pure functions (same input → same output, no side effects) where possible
- Avoid flag arguments (`doSomething(true, false)`); use separate named functions instead

## 3. Error Handling

- Never silently swallow errors; always log or propagate them
- Use typed/domain errors rather than generic `Error` objects where appropriate
- Validate inputs at the boundary of your system (API layer, service entry points)
- Prefer failing fast: throw/return early when preconditions aren't met
- Provide actionable error messages: include what happened, why, and how to fix it

## 4. Code Organization

- Group related logic together; keep files focused on a single concern
- Follow your project's established module/folder structure
- Separate concerns: keep data access, business logic, and presentation distinct
- Avoid deep nesting; refactor to early returns or helper functions
- Delete dead code; don't comment it out

## 5. Comments & Documentation

- Write self-documenting code first; add comments to explain *why*, not *what*
- Keep comments up-to-date; stale comments are worse than none
- Document public APIs with JSDoc/docstrings: purpose, params, return value, exceptions
- Add a brief module-level comment explaining the purpose of the file when non-obvious

## 6. Testing

- Write tests alongside new code, not after the fact
- Cover the happy path, edge cases, and error scenarios
- Keep tests independent; avoid shared mutable state between tests
- Name tests descriptively: `should return null when user not found`
- Prefer testing behavior over implementation details
- Aim for fast unit tests; reserve slow integration/e2e tests for critical paths

## 7. Performance & Safety

- Avoid premature optimization; profile before fixing
- Prefer immutable data structures to prevent accidental mutation
- Be explicit about data ownership and mutation boundaries
- Sanitize and validate all external input (user data, environment variables, API responses)
- Avoid storing sensitive data in logs, local storage, or unencrypted fields

## 8. Dependencies & Tooling

- Only add a dependency if it provides clear value over a custom implementation
- Pin dependency versions in production; use lockfiles
- Remove unused dependencies regularly
- Prefer well-maintained, widely-used packages with a small attack surface
- Keep dependencies up-to-date; subscribe to security advisories

---
name: git-workflow
description: Git branching, commit, and collaboration best practices. Use when creating branches, writing commit messages, opening pull requests, or resolving conflicts. Covers conventional commits, branch naming, and code review etiquette.
license: MIT
metadata:
  author: fulgidus
  version: "1.0.0"
---

# Git Workflow Best Practices

Guidelines for a clean, collaborative Git workflow — covering commits, branches, pull requests, and conflict resolution.

## When to Apply

Reference these guidelines when:
- Creating a new branch or feature
- Staging and writing commit messages
- Opening or reviewing a pull request
- Resolving merge conflicts

## 1. Commit Messages (Conventional Commits)

Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<optional scope>): <short summary>

[optional body]

[optional footer(s)]
```

### Types

| Type       | When to use                                    |
|------------|------------------------------------------------|
| `feat`     | A new feature                                  |
| `fix`      | A bug fix                                      |
| `docs`     | Documentation changes only                    |
| `style`    | Formatting, missing semicolons, etc.           |
| `refactor` | Code change that is neither a fix nor a feature|
| `test`     | Adding or updating tests                       |
| `chore`    | Build process, tooling, dependency updates     |
| `perf`     | Performance improvements                       |
| `ci`       | CI/CD configuration changes                   |
| `revert`   | Reverts a previous commit                      |

### Rules

- Use the **imperative mood** in the summary: "add feature" not "added feature"
- Keep the summary under **72 characters**
- Reference issue numbers in footers: `Fixes #42` or `Closes #123`
- Mark breaking changes with `BREAKING CHANGE:` in the footer or `!` after the type: `feat!:`

### Examples

```
feat(auth): add OAuth2 login with GitHub

Implements GitHub OAuth2 flow for user authentication.
Adds a new /auth/github endpoint and stores tokens securely.

Closes #45
```

```
fix(api): handle null response from payment gateway

Payment gateway occasionally returns null on timeout.
Added a guard clause to return a 503 instead of crashing.
```

## 2. Branch Naming

Use a consistent, descriptive naming convention:

```
<type>/<short-description>
```

Examples:
- `feat/user-profile-page`
- `fix/login-redirect-loop`
- `chore/upgrade-node-18`
- `docs/update-readme`
- `refactor/extract-auth-middleware`

Rules:
- Use **lowercase kebab-case**
- Keep names short but descriptive (3–6 words)
- Include an issue number when applicable: `feat/45-github-oauth`
- Never commit directly to `main`/`master` or `develop`

## 3. Branching Strategy

- **`main`** — always production-ready; protected
- **`develop`** (optional) — integration branch for features
- **Feature branches** — branch from `main` (or `develop`), merge back via PR
- **Hotfix branches** — branch from `main`, merge to both `main` and `develop`
- Delete branches after merging to keep the repo tidy

## 4. Pull Requests

- Keep PRs **small and focused** — one feature or fix per PR
- Write a clear PR description: what changed, why, and how to test
- Link related issues: `Fixes #42`
- Add screenshots or recordings for UI changes
- Request reviews from relevant stakeholders
- Address all review comments before merging
- Prefer **squash merge** for feature branches to keep history clean
- Use **merge commit** for release or long-lived branches to preserve history

### PR Description Template

```markdown
## What
Brief description of the change.

## Why
Motivation and context.

## How to Test
Steps to verify the change works.

## Screenshots (if applicable)

## Related Issues
Closes #
```

## 5. Code Review Etiquette

- Review for correctness, readability, performance, and security
- Be constructive: suggest alternatives, don't just criticize
- Distinguish blocking issues from optional suggestions (use prefixes: `nit:`, `suggestion:`, `blocking:`)
- Approve only when you're confident the change is ready
- Don't leave PRs open without a response for more than 24 hours

## 6. Conflict Resolution

- Rebase onto the target branch before opening a PR to minimize conflicts
- Resolve conflicts locally; never force-push to shared branches
- When in doubt about a conflict, discuss with the original author
- Use `git rerere` to automate re-applying conflict resolutions

## 7. Repository Hygiene

- Keep `.gitignore` up-to-date; never commit build artifacts or secrets
- Tag releases with semantic versions: `v1.2.3`
- Write a meaningful `CHANGELOG.md` (automate with `conventional-changelog`)
- Protect `main` with required reviews and CI checks

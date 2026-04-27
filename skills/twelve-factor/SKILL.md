---
name: twelve-factor
description: Apply Twelve-Factor app methodology. Use when scaffolding a new service, writing deployment config, or reviewing service architecture for operability. Do NOT trigger for frontend-only SPA projects, CLI tools, or libraries that do not run as a networked service.
---

# Twelve-Factor

## Rules

1. **Config in the environment.** Every value that varies between deploys (DB URLs, API keys, ports, feature flags) goes in env vars. Nothing is hardcoded or committed.
2. **Explicit dependencies.** Declare all dependencies in a manifest (package.json, Cargo.toml, go.mod). Never rely on implicit system packages.
3. **Stateless processes.** Processes share nothing. All persistent state lives in a backing service (DB, cache, queue). Any process instance can be killed and replaced without data loss.
4. **Dev/prod parity.** Close the gap between development and production in tools, backing services, and data. The gap is where bugs live.
5. **Logs as event streams.** Write to stdout. Never open log files. Let the platform route and store.
6. **Strict build/release/run separation.** A deployed release is immutable. Never patch a running process; build a new release.
7. **Port binding.** Export services via port binding — the app is self-contained, not injected into a server container.
8. **Disposability.** Optimise for fast startup and graceful shutdown. Processes can be started or stopped at any time.

## Anti-patterns

- Do not commit config (API keys, DSNs, environment-specific values) to the repository.
- Do not store any shared mutable state in the process — it breaks horizontal scaling.
- Do not mutate a running release in place (hotpatching, live file edits).
- Do not write application logs to disk from within the app.

## Refs

- [[wiki/beliefs/deployment]]
- [[wiki/sources/twelve-factor-app]]

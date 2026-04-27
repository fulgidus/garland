---
name: structured-logging
description: Apply structured logging conventions. Use when writing, reviewing, or configuring any log statement in application code. Do NOT trigger for test code, CLI tools printing user-facing output, or scripts where stdout is the product.
---

# Structured Logging

## Rules

1. Emit structured records (JSON or logfmt key-value pairs), never interpolated strings.
2. Attach a correlation/trace ID to every log line so any request can be fully reconstructed across services.
3. Inject context (request ID, user ID, service name, version, environment) once at the request boundary. Propagate via a context object — never pass it through every function signature.
4. Reserve log levels strictly:
   - `ERROR` — operator must act now.
   - `WARN` — worth investigating, not urgent.
   - `INFO` — key lifecycle events only (startup, shutdown, major state changes).
   - `DEBUG` — off in production.
5. Write logs to stdout/stderr. Let the platform (Docker, k8s, systemd) collect, route, and store them. Never write to files from application code.

## Anti-patterns

- Do not log free-form interpolated strings (`"user " + id + " did thing"`).
- Do not log passwords, tokens, secrets, or PII at any level, including DEBUG.
- Do not open log files directly from application code.
- Do not emit INFO for every request or every DB call — that is DEBUG territory.
- Do not invent per-service log formats; pick one structured format and apply it everywhere.

## Refs

- [[wiki/beliefs/logging]]
- [[wiki/sources/logging-sucks]]
- [[wiki/sources/twelve-factor-app]]

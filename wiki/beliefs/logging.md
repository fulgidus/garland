---
topic: logging
updated: 2026-04-27
---

# Logging

## Position

Logs are a machine-readable event stream, not prose written for the developer who wrote the code. Every log line should be a structured record with consistent fields, emitted at the right level, enriched with request-scoped context at the boundary, and correlated across services via a trace/request ID. Unstructured string interpolation makes logs unsearchable and operators' lives miserable.

## Rules

- DO: emit structured logs (JSON or logfmt key-value pairs). [[sources/logging-sucks]]
- DO: attach a correlation/trace ID to every log line so a full request can be reconstructed. [[sources/logging-sucks]]
- DO: inject context (request ID, user ID, service name, version) once at the request boundary; propagate via context object. [[sources/logging-sucks]]
- DO: reserve levels strictly — ERROR = act now, WARN = investigate, INFO = key lifecycle events only, DEBUG = off in production. [[sources/logging-sucks]]
- DO: treat the log output as a stream (write to stdout/stderr); let the platform route and store it. [[sources/twelve-factor-app]]
- DON'T: log sensitive data (passwords, tokens, PII) at any level. [[sources/logging-sucks]]
- DON'T: use free-form interpolated strings as log messages. [[sources/logging-sucks]]
- DON'T: write logs directly to files from application code; that is the platform's job. [[sources/twelve-factor-app]]

## Open questions

- Where is the right boundary for context injection in frameworks that don't have a clean request middleware layer?

## Conflicts

_(none)_

## Sources

- [[sources/logging-sucks]]
- [[sources/twelve-factor-app]]

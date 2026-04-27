---
clipped: 2026-04-27
url: https://loggingsucks.com/
raw: ../../raw/logging-sucks.md
---

# Logging Sucks. And Here's How to Make It Better.

## Author / context

Boris Tane, nominal.dev, December 2024. Practitioner post diagnosing why application logging is painful in production and offering a structured alternative.

## Summary

Most application logs are unstructured strings written for the developer who wrote the code, not for the operator who will read them at 2am. The post argues that logs should be structured key-value event records — emitted consistently, enriched with context at the request boundary, correlated across services via trace/request IDs, and treated as a stream rather than a file. The practical payoff is that logs become queryable and actionable rather than noise to grep through.

## Key precepts

- Emit structured logs (JSON or logfmt key-value), not interpolated strings.
- Attach context (request ID, user ID, service name, version) at the boundary once; propagate via context object, not function parameters.
- Use a correlation/trace ID on every line so a full request can be reconstructed.
- Reserve log levels strictly: ERROR = operator must act, WARN = worth investigating, INFO = key lifecycle events only, DEBUG = off in production.
- Never log sensitive data (passwords, tokens, PII) even at DEBUG level.
- Treat the log stream as machine-readable input to a collector, not as text to tail.

## Verbatim anchors

> "2024-12-20T03:14:22.847Z INFO HttpServer started successfully binding=0.0.0.0:3000 pid=28471 env=production version=2.4.1 node_env=production cluster_mode=enabled workers=4"

> "request_id=req_8f7a2b3c trace_id=abc123def456"

## Topics

- [[../beliefs/logging]]

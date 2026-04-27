---
title: "Twelve-Factor App"
parent: "Sources"
grand_parent: "Wiki"
---

# The Twelve-Factor App

## Author / context

Adam Wiggins, Heroku, 2012 (last updated 2017). Distilled from direct experience building and operating hundreds of thousands of SaaS apps on the Heroku platform.

## Summary

Twelve patterns that make a web service deployable, portable, scalable, and operable without heroics. The patterns address the full lifecycle: codebase management, dependency isolation, config externalisation, backing service abstraction, build/release/run separation, stateless processes, port-bound service exposure, process-model scaling, graceful startup/shutdown, dev/prod parity, log streaming, and admin task isolation. Most production pain can be traced to violating one of these twelve contracts.

## Key precepts

- Config belongs in the environment (env vars), never hardcoded or in committed files.
- Declare and isolate dependencies explicitly; never rely on implicit system packages.
- Processes must be stateless; all shared state lives in a backing service.
- Keep dev, staging, and production as similar as possible — the gap between them is where bugs live.
- Treat logs as event streams: write to stdout, let the platform collect and route.
- Strictly separate the build, release, and run stages; never mutate a deployed release.

## Verbatim anchors

> "Store config in the environment"

> "Treat logs as event streams"

> "Keep development, staging, and production as similar as possible"

> "Execute the app as one or more stateless processes"

## Topics

- [[deployment]]

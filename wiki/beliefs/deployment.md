---
topic: deployment
updated: 2026-04-27
---

# Deployment

## Position

A service that is hard to deploy, scale, or debug in production was designed that way. The Twelve-Factor methodology defines the contracts a service must honour to be operable without heroics: config in the environment, stateless processes, explicit dependencies, parity between environments, and logs as a stream. Violating any of these contracts transfers operational pain from the machine to the human.

## Rules

- DO: store all config in environment variables; never hardcode or commit configuration. [[sources/twelve-factor-app]]
- DO: declare and isolate dependencies explicitly; never rely on implicit system-level packages. [[sources/twelve-factor-app]]
- DO: make processes stateless; all shared state belongs in a backing service (database, cache, queue). [[sources/twelve-factor-app]]
- DO: keep dev, staging, and production as similar as possible — the gap between them is where bugs live. [[sources/twelve-factor-app]]
- DO: write logs to stdout; let the platform collect, route, and store them. [[sources/twelve-factor-app]] [[sources/logging-sucks]]
- DO: strictly separate build, release, and run stages; treat a deployed release as immutable. [[sources/twelve-factor-app]]
- DO: expose services via port binding, not server-managed injection. [[sources/twelve-factor-app]]
- DON'T: store session state or any shared mutable state in the process; it breaks horizontal scaling. [[sources/twelve-factor-app]]
- DON'T: mutate a running release; build a new release and deploy it. [[sources/twelve-factor-app]]
- DON'T: write application logs to files; that couples the app to the filesystem and the deployment environment. [[sources/twelve-factor-app]]

## Open questions

- How does Factor III (env vars for config) interact with secrets management systems (Vault, AWS SSM) at scale?
- Does the stateless process model (Factor VI) still hold cleanly for long-running stateful workloads like ML inference servers?

## Conflicts

_(none)_

## Sources

- [[sources/twelve-factor-app]]

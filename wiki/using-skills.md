---
title: "Using Skills"
parent: "Wiki"
nav_order: 3
---

# Using Skills

Skills in `skills/` are distilled from wiki beliefs and can be attached to any project
that runs an agent supporting the [Agent Skills standard](https://agentskills.io/specification).

## Install: make all skills globally available in pi

Create (or update) `~/.pi/settings.json`:

```json
{
  "skills": ["/home/fulgidus/Documents/garland/skills"]
}
```

Pi will discover every `skills/<name>/SKILL.md` automatically on startup.
Any skill you distill here is immediately available in all future pi sessions — no copy, no symlink.

## Install: per-project (select skills only)

Add to `.pi/settings.json` inside the target project:

```json
{
  "skills": [
    "/home/fulgidus/Documents/garland/skills/branded-types",
    "/home/fulgidus/Documents/garland/skills/tdd"
  ]
}
```

## Install: one-off via CLI

```bash
pi --skill /home/fulgidus/Documents/garland/skills/branded-types
```

## Load a skill by name in session

Once installed, force-load a skill with its slash command:

```
/skill:branded-types
/skill:tdd
/skill:structured-logging
/skill:simple-design
/skill:twelve-factor
```

## Available skills

| Skill | Triggers when |
| ----- | ------------- |
| `branded-types` | writing TS code with domain-meaningful primitives |
| `tdd` | writing any new function or feature |
| `structured-logging` | writing or reviewing any log statement |
| `simple-design` | refactoring, code review, abstraction decisions |
| `twelve-factor` | scaffolding or configuring a networked service |
| `obscura` | fetching dynamic pages or scraping URLs in bulk |

## How pi decides to load a skill

Pi reads the `description` field of every installed skill at startup and injects them
into the system prompt. The agent picks the relevant skill from that list based on the
task. If it doesn't auto-load, use `/skill:<name>` to force it.

## Adding a new skill

```
distill skill <name> from <belief-topic>
```

The skill is written to `skills/<name>/SKILL.md` and immediately available
via the global settings path above.

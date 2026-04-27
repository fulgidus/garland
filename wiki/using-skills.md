---
title: "Using Skills"
parent: "Wiki"
nav_order: 3
---

# Using Skills

Skills in `skills/` are distilled from wiki beliefs and installable into any agent
(pi, Claude Code, Cursor, OpenCode, etc.) via the
[`skills` CLI](https://www.npmjs.com/package/skills).

## Install all skills globally (recommended)

```bash
# from GitHub (after pushing)
bunx skills add fulgidus/garland -g -a pi

# or from local path
bunx skills add /home/fulgidus/Documents/garland -g -a pi
```

`-g` installs to `~/.pi/agent/skills/` (global, all sessions).
Omit `-g` to install into the current project's `.pi/skills/` instead.

## Install specific skills only

```bash
bunx skills add fulgidus/garland --skill branded-types --skill tdd -g -a pi
```

## Install to multiple agents at once

```bash
bunx skills add fulgidus/garland -g -a pi -a claude-code -a opencode
```

## List what's installed

```bash
bunx skills list
bunx skills ls -g   # global only
```

## Update after distilling new skills

```bash
bunx skills update -g -y
```

## Remove a skill

```bash
bunx skills remove simple-design -g
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

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
bun x skills add fulgidus/garland -g -a pi --yes
```

To update after pushing new distilled skills:

```bash
bun x skills update -g -y
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

# SPEC.md — Bootstrap the `cognitive-base` repo

## Goal

Create a new git repository that implements the **Clip → Absorb → Distill →
Attach** pipeline described in `cognitive-base-proposal.md`. This SPEC produces
the *empty but operational* substrate: layout, seed files, templates, and a
single bootstrap commit. No sources are ingested and no skills are distilled at
this stage — those happen later, on demand, via the workflows defined in
`AGENTS.md`.

The output of this SPEC is what the user clones into a working directory before
running their agent for the first ingest.

---

## Deliverable

A git repository named `cognitive-base` containing:

- The directory layout in [§ Repo layout](#repo-layout).
- All seed files in [§ Files to create](#files-to-create), with the exact
  content given.
- Three template files under `wiki/_templates/` and `skills/_template/`.
- One initial commit on the `main` branch with the message
  `chore: bootstrap cognitive base`.

No remote is configured. No PR is opened. No CI, no license, no tooling beyond
plain markdown and git.

---

## Repo layout

```
cognitive-base/
├── .gitignore
├── AGENTS.md
├── README.md
├── SPEC.md                         # this file, copied verbatim
├── raw/
│   └── .gitkeep
├── wiki/
│   ├── index.md
│   ├── log.md
│   ├── _templates/
│   │   ├── source.md
│   │   └── belief.md
│   ├── beliefs/
│   │   └── .gitkeep
│   ├── entities/
│   │   └── .gitkeep
│   └── sources/
│       └── .gitkeep
└── skills/
    └── _template/
        └── SKILL.md
```

Empty leaf directories are kept in git via `.gitkeep`. Underscore-prefixed
directories (`_templates`, `_template`) are reserved for scaffolding the agent
copies from — they are never modified by the `ingest` or `distill` workflows.

---

## Files to create

Each file below must be created with the **exact content shown**. Where a
template contains placeholders (`<...>`), they are part of the template and must
be preserved literally.

### `.gitignore`

```
.DS_Store
*.swp
*.tmp
node_modules/
.opencode/
.pi/
```

### `README.md`

```markdown
# cognitive-base

Personal substrate for distilling articles, posts, and talks I agree with into
`SKILL.md` files attachable to projects.

Three layers:

| Layer       | Path       | Owner              | Mutability                      |
| ----------- | ---------- | ------------------ | ------------------------------- |
| Sources     | `raw/`     | Obsidian Clipper   | Immutable                       |
| Knowledge   | `wiki/`    | Agent (per AGENTS) | Mutable, append-mostly          |
| Artifacts   | `skills/`  | Agent (per AGENTS) | Mutable, distilled from `wiki/` |

Workflows are defined in `AGENTS.md`. Bootstrap rationale and end-to-end
example are in `SPEC.md`.

Driven via any agent runner that consumes `AGENTS.md` (e.g. opencode, pi-agent).
```

### `AGENTS.md`

```markdown
# Personal cognitive base

This repo is my personal base of technical beliefs. Three layers:

- `raw/`: immutable sources clipped from Obsidian Web Clipper. Never modify.
- `wiki/`: knowledge base that YOU maintain. `beliefs/` per topic,
  `entities/` per actor, `sources/` per source.
- `skills/`: `SKILL.md` artifacts distilled from the wiki, used in projects.

Underscore-prefixed directories (`_templates/`, `_template/`) are scaffolding.
Copy from them; never modify them.

## Workflow: ingest

When I say `ingest raw/<file>`:

1. Read the source. Write a one-page summary to `wiki/sources/<slug>.md` based
   on `wiki/_templates/source.md`, with a link back to the raw file and at
   least one short verbatim quote per key precept.
2. Identify the operational precepts (what to do, what not to do, why).
3. For every topic touched, update `wiki/beliefs/<topic>.md` (creating it from
   `wiki/_templates/belief.md` if needed):
   - if the page exists, integrate the new claims;
   - if a new claim contradicts an existing one, keep both and flag with
     `> CONFLICT:` plus a one-line note.
   - cite sources as `[[sources/<slug>]]` next to each claim.
4. Update `wiki/index.md` and append a line to `wiki/log.md` in the format
   `## [YYYY-MM-DD] ingest | <title>`.
5. Summarize what changed in chat. Do not proceed further without my OK.

## Workflow: distill

When I say `distill skill <name> from <topic|sources>`:

1. Read the relevant `wiki/beliefs/` pages.
2. Create `skills/<name>/SKILL.md` from `skills/_template/SKILL.md`, optimized
   for **minimum context impact**:
   - frontmatter `name` + `description` (one trigger-friendly sentence).
   - body: imperative rules, no motivational prose, no explanations of "why".
   - ~50 useful lines max. If more detail is needed, use sibling files in the
     same folder, referenced from `SKILL.md`.
3. The `description` MUST state when the skill must trigger and when it must
   NOT. It is the discriminator the loader uses.
4. Append a line to `wiki/log.md` in the format
   `## [YYYY-MM-DD] distill | <skill-name>`.
5. Show me a diff before writing.

## Workflow: lint

When I say `lint wiki`:

- Find contradictions across `beliefs/` pages.
- Find claims with no `[[sources/...]]` backing.
- Find orphan pages (not referenced from `index.md` or any belief).
- Find concepts mentioned but lacking a page.

Propose actions in chat. Do not execute.

## House rules

- Never modify `raw/` or any underscore-prefixed directory.
- Never open PRs. Branch + diff for human review.
- English everywhere — chat, commits, wiki, skills. The repo must be portable
  across any team or project.
- Conventional commits, imperative mood, no emoji, ≤100-char subject.
- Markdown tables: spaced columns, aligned separators.
- No code execution at this stage. Markdown only.
```

### `SPEC.md`

Copy this file verbatim into the repo root.

### `raw/.gitkeep`

Empty file.

### `wiki/index.md`

```markdown
# Wiki index

Catalog of beliefs and entities. Maintained by the agent during `ingest`.

## Beliefs

_(empty — no sources ingested yet)_

## Entities

_(empty)_

## Sources

_(empty)_
```

### `wiki/log.md`

```markdown
# Activity log

Append-only timeline. One line per `ingest` or `distill`.

## [YYYY-MM-DD] bootstrap | repo initialized
```

The agent must replace `YYYY-MM-DD` with the actual bootstrap date in ISO 8601.

### `wiki/_templates/source.md`

```markdown
---
clipped: YYYY-MM-DD
url: <original-url>
raw: ../../raw/<filename>.md
---

# <Title>

## Author / context

<one line: who wrote it, where, when, why it matters>

## Summary

<one paragraph in your own words. No quoting here.>

## Key precepts

- <precept 1>
- <precept 2>

## Verbatim anchors

> "<short literal quote that anchors precept 1>"

> "<short literal quote that anchors precept 2>"

## Topics

- [[../beliefs/<topic>]]
```

### `wiki/_templates/belief.md`

```markdown
---
topic: <topic-slug>
updated: YYYY-MM-DD
---

# <Topic>

## Position

<one paragraph stating the stance, in plain language>

## Rules

- DO: <rule>. [[sources/<slug>]]
- DON'T: <anti-pattern>. [[sources/<slug>]]

## Open questions

- <question>

## Conflicts

> CONFLICT: <claim A> ([[sources/<slug-a>]]) vs <claim B> ([[sources/<slug-b>]]).
> Resolution: <pending | A | B | both apply in different contexts>.

## Sources

- [[sources/<slug>]]
```

### `wiki/beliefs/.gitkeep`, `wiki/entities/.gitkeep`, `wiki/sources/.gitkeep`

Empty files.

### `skills/_template/SKILL.md`

```markdown
---
name: <skill-name>
description: <one sentence: when this skill MUST trigger and when it MUST NOT>
---

# <Skill name>

## Rules

1. <imperative rule>
2. <imperative rule>

## Anti-patterns

- <thing the agent must not do, even if asked>

## Refs

<internal pointers to wiki, for human readers only — the agent should not need
these at runtime>
- [[wiki/beliefs/<topic>]]
```

---

## Workflow primitives the repo must support

After bootstrap, the following commands (issued in chat to whichever agent
consumes `AGENTS.md`) must work without further setup:

| Command                                  | Effect                                   |
| ---------------------------------------- | ---------------------------------------- |
| `ingest raw/<file>`                      | Updates `wiki/` from a clipped source    |
| `distill skill <name> from <topic>`      | Creates `skills/<name>/SKILL.md`         |
| `lint wiki`                              | Reports inconsistencies, no writes       |

The agent already has the rules in `AGENTS.md` and the templates in
`_templates/` / `_template/`. No additional configuration is required.

---

## Acceptance criteria

- [ ] `cognitive-base/` exists and is a valid git repository.
- [ ] Default branch is `main`.
- [ ] Tree matches the layout in [§ Repo layout](#repo-layout) exactly.
- [ ] All files in [§ Files to create](#files-to-create) exist with the exact
      content specified.
- [ ] `wiki/log.md` has the bootstrap date filled in (ISO 8601).
- [ ] All `.gitkeep` files are present and empty.
- [ ] `raw/`, `wiki/beliefs/`, `wiki/entities/`, `wiki/sources/` contain only
      `.gitkeep` (no real content).
- [ ] `skills/` contains only `_template/SKILL.md`.
- [ ] One commit on `main` with message `chore: bootstrap cognitive base`.
- [ ] No remote configured.
- [ ] No emoji anywhere in tracked files.

---

## Constraints

- **Markdown and git only.** No package manager, no CI, no scripts, no hooks.
  Tooling can come later, when the first script genuinely needs to land.
- **No license file** at this stage. The repo is private by default; license
  decision is deferred.
- **No `prek` config** yet. Will be added when the first script appears.
- **No content seeding.** Do not invent sample sources, beliefs, or skills.
  The repo must be empty of real content — only scaffolding.
- **No author identity assumptions.** Use whatever git config is already on
  the host. Do not set `user.name` / `user.email`.
- **One commit.** Do not split bootstrap into multiple commits.

---

## Out of scope

The following are explicitly NOT part of this SPEC and must not be done:

- Ingesting any source (including `loggingsucks.com` from the proposal example).
- Creating any real `SKILL.md` (only the template).
- Configuring a git remote, opening a PR, or pushing anywhere.
- Adding CI, badges, license, or contributor docs.
- Implementing the agent runner integration (handled by `pi-agent` /
  `pi-llm-wiki` / opencode externally).
- Adding a `prek.toml` or any pre-commit config.
- Defining a skill distribution mechanism (submodule, npm, symlink) — that is
  a per-project decision, not a repo-bootstrap concern.

---

## Done when

The user can `cd cognitive-base && <agent-runner>` and immediately issue an
`ingest raw/<file>` command after dropping a clipped article into `raw/`,
without needing any further setup.

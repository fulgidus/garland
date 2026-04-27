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
- Conventional commits, imperative mood, no emoji, <=100-char subject.
- Markdown tables: spaced columns, aligned separators.
- No code execution at this stage. Markdown only.

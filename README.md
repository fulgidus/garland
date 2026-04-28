# Garland
<div align="center">
     <br>
     <img src="garland-logo.svg" width="128" />
     <br><br>
     <p>Personal substrate for distilling articles, posts, and talks I agree with into <code>SKILL.md</code> files
 attachable to projects.</p>
   </div>

---

Three layers:

| Layer       | Path       | Owner              | Mutability                      |
| ----------- | ---------- | ------------------ | ------------------------------- |
| Sources     | `raw/`     | Obsidian Clipper   | Immutable                       |
| Knowledge   | `wiki/`    | Agent (per AGENTS) | Mutable, append-mostly          |
| Artifacts   | `skills/`  | Agent (per AGENTS) | Mutable, distilled from `wiki/` |

---

Workflows are defined in `AGENTS.md`. Bootstrap rationale and end-to-end
example are in `SPEC.md`.

Driven via any agent runner that consumes `AGENTS.md` (e.g. opencode, pi-agent).

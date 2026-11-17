# Template: AGENTS.md Hub

> Use for: `AGENTS.md` — the single source of truth that every AI agent reads first
> Location: repo root, with a one-line `CLAUDE.md` next to it (see CLAUDE.md Companion below)

---

## Structure

````markdown
# [Project Name] — Project Hub

> Single source of truth for AI agents working on this codebase. Every agent reads this file first.
> `CLAUDE.md` contains only the import `@AGENTS.md`, so Claude Code loads this same file.
> For the full documentation index, see [docs/_index.md](docs/_index.md).

---

## Identity

| Field | Value |
|-------|-------|
| Name | [project name] |
| Type | [project type] |
| Stack | [key technologies] |
| Version | [current version] |
| Repo | [repo URL] |

---

## Stable Rules

> Non-negotiable. They apply to every task and every agent, and task-level prompts do not relax them.
> Change this section only with explicit human approval.

1. **[Rule 1]** — [security, compliance, or permanent project constraint]
2. **[Rule 2]** — [constraint]
... (one line per rule; when a rule needs explanation, keep the line here and link to a doc)

**Coding behavior** — think before coding, simplicity first, surgical changes, goal-driven execution. Read the full text before changing any file: [.claude/rules/coding-behavior-rules.md](.claude/rules/coding-behavior-rules.md).

---

## Read First

- [docs/_index.md](docs/_index.md) — Full documentation map
- [docs/project/overview.md](docs/project/overview.md) — Project identity and stack
- [.claude/skills/updating-docs/SKILL.md](.claude/skills/updating-docs/SKILL.md) — Doc-update procedure; follow it before writing in `docs/`
- [README.md](README.md) — User-facing introduction

---

## Task Routing

> If you are working on X → read Y first.

| Task | Read First |
|------|------------|
| [task type] | [docs/path/file.md](docs/path/file.md) |

---

## Directory Tree (Authoritative)

```text
[project-root]/
├── .claude/
│   ├── rules/
│   │   └── coding-behavior-rules.md
│   └── skills/
│       └── updating-docs/
│           └── SKILL.md
├── docs/
│   ├── _index.md
│   ├── project/
│   ├── architecture/
│   ├── features/
│   └── ...
├── AGENTS.md
├── CLAUDE.md
└── decisions.md
```

> Keep this tree updated when top-level structure changes.

---

## Quick Commands

```bash
[command to run]
[command to test]
[command to build]
```

---

## Working Rules

1. **[Rule 1]** — [why]
2. **[Rule 2]** — [why]
3. **[Rule 3]** — [why]
... (keep to 5-8 rules, repo-specific)

> Put only operational/session rules here.
> Put non-negotiable rules in `## Stable Rules` above.

## Hybrid Strategy

- Preserve installer core requirements (phase flow, safety gates, stable rules)
- Apply inspired-layer practices (modular docs, useful cross-links, living updates, rationale-first content)
- Prefer high-signal docs; avoid low-value expansion

---

## Doc Workflow

When creating or significantly modifying a feature:

1. **Spec + Plan** — create in the repo's chosen design/planning location (if using that workflow)
2. **Feature doc** — create in `docs/features/` or appropriate category
3. **Design Origin** — link to spec/plan if applicable
4. **Link here** — add entry to Documentation Map below
5. **Link related docs** — add relative Markdown links in the Related section

### Where to put docs

| Category | Path | When |
|----------|------|------|
| Feature workflow | `docs/features/` | New user-facing behavior |
| Architecture | `docs/architecture/` | Structural changes |
| Reference | `docs/reference/` | New constants, config options |
| Project | `docs/project/` | Known issues, project changes |

---

## Documentation Map

### Project
- [docs/project/overview.md](docs/project/overview.md) — [one-line description]
- [docs/project/repository-map.md](docs/project/repository-map.md) — [one-line description]
... (only include categories that have docs)

### Architecture
- [docs/architecture/<name>.md](docs/architecture/<name>.md) — [one-line description]

### Features
- [docs/features/<name>.md](docs/features/<name>.md) — [one-line description]

### Reference
- [docs/reference/<name>.md](docs/reference/<name>.md) — [one-line description]

---

## Key Warnings

- **[Warning 1]** — see [docs/path/detail.md](docs/path/detail.md)
- **[Warning 2]** — see [docs/path/detail.md](docs/path/detail.md)

---

## Definition of Done

- [ ] Change implemented with minimal scope
- [ ] Related docs updated
- [ ] Verification commands run for affected stack
  - TypeScript repos: `tsc --noEmit`
- [ ] Commit is scoped to one issue/change set
- [ ] `decisions.md` updated for lasting design choices
- [ ] `AGENTS.md` updated to match current project state

---

## Session Closeout

At the end of each work session:

1. Update `AGENTS.md` according to the current project state (`## Stable Rules` changes only with human approval)
2. Update `decisions.md` with new stable decisions
3. Re-check Documentation Map and links

---

## Related Files

- [README.md](README.md) — User-facing intro
- [decisions.md](decisions.md) — Design decisions log
- `CLAUDE.md` — One-line import of this file for Claude Code
````

## CLAUDE.md Companion

Create `CLAUDE.md` in the repo root with exactly this content:

```markdown
@AGENTS.md
```

- Claude Code expands the import at session start, so it loads the same hub as every other agent
- A `CLAUDE.md` with content of its own makes Claude Code read that file instead of `AGENTS.md`, and the two hubs drift apart — keep it to the import line
- Use the import, not a symlink: on Windows, Git checks a committed symlink out as a one-line text file unless `core.symlinks` is enabled
- Only instructions that apply to Claude Code alone (for example, a Claude-only slash command) may follow the import line; everything that applies to every agent belongs in `AGENTS.md`

## Guidelines

- Keep AGENTS.md under 200 lines — it loads into every session of every agent, so move detail into `docs/` and link to it
- Every link must point to a real file
- Use standard relative Markdown links; `AGENTS.md` sits at the repo root, so link text and href are the same path
- Stable Rules hold only non-negotiable constraints, one line each, inline — `AGENTS.md` is the one file every agent loads
- Working Rules must be specific to THIS repo (no generic rules)
- Key Warnings should point to docs that explain the risk
- Doc Workflow section must exist so AI knows to auto-create docs
- Include and maintain a directory tree to reduce path confusion
- Add/maintain a DoD + Session Closeout section
- For Task Routing rows, derive tasks from Trigger sections across created docs
- Use one row per distinct task type
- In Task Routing, link the real file in the Read First column
- If adding hybrid guidance, keep it short and operational (not conceptual essays)

---

## Related

- [INSTALL.md](../INSTALL.md) — Main instruction flow that sets up AGENTS.md
- [TEMPLATES/index-doc.md](index-doc.md) — The second navigation hub after AGENTS.md
- [PHASES/02-design.md](../PHASES/02-design.md) — Phase that designs the AGENTS.md structure
- [PHASES/03-implement.md](../PHASES/03-implement.md) — Phase that creates AGENTS.md and CLAUDE.md

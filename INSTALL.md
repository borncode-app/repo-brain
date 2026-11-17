# INSTALL — AI Agent Instructions

> Read this file FIRST. Follow phases in order.
> Do NOT skip phases. Each phase builds on the previous one.

---

## Overview

You are installing a repo brain into this repository: an `AGENTS.md` hub that every AI agent reads first, plus a linked `docs/` knowledge base. You will:

1. **Analyze** the repo (do NOT assume anything)
2. **Design** a doc tree tailored to this specific codebase
3. **Implement** docs, hub, stable rules, and decisions log
4. **Optimize links** in `AGENTS.md` and `docs/` for graph cleanliness and token efficiency
5. **Clean up** installer artifacts and obsolete files (optional, user-approved)

## Before You Start

Check which flow applies:

- **The repo has the v1 layout** — it was installed with `install-obsidian`: `CLAUDE.md` holds a `## Documentation Map` and `docs/_index.md` exists → stop here and follow [UPGRADE.md](UPGRADE.md).
- **Anything else** → continue with this file.

## One Hub for Every Agent (mandatory)

- **`AGENTS.md` is the single source of truth.** Project identity, stable rules, task routing, and the documentation map live there, because it is the one instruction file every agent loads.
- **`CLAUDE.md` holds one line: `@AGENTS.md`.** Claude Code expands that import at session start, so it reads the same hub. A `CLAUDE.md` with content of its own would make Claude Code read it instead of `AGENTS.md`.
- **An existing `AGENTS.md` is the hub.** Keep it, restructure it in place, and preserve its content.
- **Legacy instruction files are sources.** An existing `CLAUDE.md` with content, `.claude/rules/*`, and other agent-specific instruction files (for example `.github/copilot-instructions.md`, `.cursorrules`, `.cursor/rules/`, `GEMINI.md`) are consolidated into `AGENTS.md` or `docs/`, section by section, with evidence.

## Hybrid Operating Model (mandatory)

Execute all work with this model:

- **Installer core (required):** keep phase order, approval gates, stable rules in the hub, migration safety, and validation checklists
- **Inspired layer (recommended):** create small focused docs, preserve meaningful cross-links, keep docs as living knowledge, and write context/rationale first

Do not treat the inspired layer as a replacement for installer core requirements.

## Constraints

- **Do NOT create empty placeholder files** — every doc must have real content
- **Do NOT duplicate information** — link to existing docs instead of copying
- **Do NOT hardcode assumptions** — analyze the repo to discover its structure
- **Do NOT skip human approval** — present your design before implementing
- **Do NOT overwrite existing docs** unless the human explicitly approves
- **Do NOT scatter stable rules across agent-specific folders** — keep them inline in `AGENTS.md` → `## Stable Rules`
- **Do NOT put content in `CLAUDE.md`** — it holds the import `@AGENTS.md`; only instructions that apply to Claude Code alone may follow it
- **Do NOT write `[[wiki-links]]` or bare paths as links** — use standard relative Markdown links (see [PRINCIPLES.md](PRINCIPLES.md), principle 5)
- **Do NOT create low-signal doc sprawl** — every new doc must have clear value and maintenance intent
- **Do NOT replace rationale with file summaries** — capture why/tradeoffs, not only where code lives

## Installation Mode (required)

Choose one mode before Phase 2 and include it in the design proposal.

### Mode: `strict` (full-standard structure)
- Create the standard category structure from [README.md](README.md): `project`, `architecture`, `features`, `integrations`, `build`, `testing`, `reference`
- Create at least one real-content doc in each category, or explicitly link existing docs that satisfy the category
- Use this mode when the human expects the full standardized structure

### Mode: `adaptive`
- Keep the current behavior from [PRINCIPLES.md](PRINCIPLES.md): create only categories justified by the repo analysis
- Skip non-applicable categories
- Use this mode when minimal, structure-following documentation is preferred

If the human does not specify a mode, default to `strict`.

## Phase Sequence

| Phase | File | Description |
|-------|------|-------------|
| 1: ANALYZE | [PHASES/01-analyze.md](PHASES/01-analyze.md) | Explore repo structure, identify key folders, subsystems, entry points, existing instruction files |
| 2: DESIGN | [PHASES/02-design.md](PHASES/02-design.md) | Propose doc tree, AGENTS.md outline, migration plan |
| 3: IMPLEMENT | [PHASES/03-implement.md](PHASES/03-implement.md) | Create docs, write content, add links, set up hub with stable rules, CLAUDE.md import, and decisions log |
| 4: OPTIMIZE LINKS | [PHASES/04-optimize-links.md](PHASES/04-optimize-links.md) | Final link-quality pass: remove duplicate/valueless links, keep graph clean |
| 5: CLEANUP | [PHASES/05-cleanup.md](PHASES/05-cleanup.md) | Remove installer artifacts and obsolete files (after human approval) |

## How to Execute

1. Read [PRINCIPLES.md](PRINCIPLES.md) to understand the design philosophy
2. Read [PHASES/01-analyze.md](PHASES/01-analyze.md) and execute it fully
3. Present your analysis to the human, wait for acknowledgment
4. Read [PHASES/02-design.md](PHASES/02-design.md) and execute it fully
5. Present your proposed doc tree to the human, wait for approval
6. Read [PHASES/03-implement.md](PHASES/03-implement.md) and execute it fully
7. Ensure `decisions.md` is updated with notable design choices from Phase 3
8. Present the result for final review
9. Read [PHASES/04-optimize-links.md](PHASES/04-optimize-links.md) and run the link optimization pass
10. Read [PHASES/05-cleanup.md](PHASES/05-cleanup.md) and execute it after human approves the review

### Hybrid Practicality Gate (apply in every phase)

Before moving to the next phase, verify:

1. **Systematic**: required phase outputs and checks are complete
2. **Flexible**: chosen docs reflect repo reality, not template pressure
3. **Signal over volume**: no unnecessary doc proliferation
4. **Rationale present**: important docs include context/decision reasoning

## Templates

Use files in [TEMPLATES/](TEMPLATES/) as structure guides. Each template defines:
- What sections a doc type should have
- What questions it should answer
- How it should link to other docs

| Template | Purpose |
|----------|---------|
| [TEMPLATES/architecture-doc.md](TEMPLATES/architecture-doc.md) | Structural patterns and subsystem design |
| [TEMPLATES/build-doc.md](TEMPLATES/build-doc.md) | Build process, packaging, release |
| [TEMPLATES/feature-doc.md](TEMPLATES/feature-doc.md) | User-facing feature workflows |
| [TEMPLATES/hub-agents-md.md](TEMPLATES/hub-agents-md.md) | AGENTS.md hub structure and its one-line CLAUDE.md companion |
| [TEMPLATES/index-doc.md](TEMPLATES/index-doc.md) | Documentation navigation hub |
| [TEMPLATES/integration-doc.md](TEMPLATES/integration-doc.md) | External tools and libraries |
| [TEMPLATES/migration-map.md](TEMPLATES/migration-map.md) | Section-by-section migration mapping (legacy instruction files and other docs) |
| [TEMPLATES/project-doc.md](TEMPLATES/project-doc.md) | Project-level knowledge |
| [TEMPLATES/reference-doc.md](TEMPLATES/reference-doc.md) | Config, constants, conventions |
| [TEMPLATES/testing-doc.md](TEMPLATES/testing-doc.md) | Testing strategy and conventions |

Templates are NOT pre-filled content. You must fill them with real information from the repo.

## Completion Checklist

High-level verification — see [PHASES/03-implement.md](PHASES/03-implement.md) for the full detailed checklist.

- [ ] All approved docs created with real content
- [ ] AGENTS.md and docs/_index.md created as hubs
- [ ] CLAUDE.md contains the import `@AGENTS.md`
- [ ] Stable rules written inline in `AGENTS.md` → `## Stable Rules`
- [ ] `decisions.md` created/updated with key design decisions
- [ ] Mode requirements satisfied (`strict` full standard categories OR `adaptive` justified subset)
- [ ] Relative Markdown links connect related docs
- [ ] Instruction-file migration coverage is 100% (if the repo had an `AGENTS.md` or legacy instruction files)
- [ ] No critical information from existing instruction files is lost
- [ ] No empty placeholder files or hardcoded assumptions
- [ ] Link optimization completed for `AGENTS.md` + `docs/` (duplicate/valueless links removed)
- [ ] Cleanup completed (installer and obsolete files removed or preserved per user choice)
- [ ] Hybrid practicality gate passed at each phase (systematic + flexible + high-signal + rationale-first)

## Definition of Done

Installation is complete only when all of the following are true:

1. `AGENTS.md` exists and is usable as the project hub
2. `docs/_index.md` exists and links to the full documentation set
3. Stable rules exist inline in `AGENTS.md` → `## Stable Rules`
4. `decisions.md` exists for persistent design rationale
5. Core docs exist per selected mode:
    - `strict`: all standard categories from [README.md](README.md) are represented
    - `adaptive`: only analysis-justified categories are present (with rationale in Phase 2 output)
6. If the repo had an `AGENTS.md` or legacy instruction files, all meaningful sections are mapped and migrated with evidence
7. Final link optimization pass completed on `AGENTS.md` + `docs/`
8. Cleanup completed (installer and obsolete files removed or preserved per user choice)
9. Post-install validation checklist is complete with no unresolved critical failures
10. Hybrid model is respected: installer core preserved and inspired layer applied without drift
11. `updating-docs` skill installed at `./.claude/skills/updating-docs/SKILL.md` and referenced by `AGENTS.md` Read First
12. `CLAUDE.md` contains the import `@AGENTS.md` and no instructions that apply to other agents

## Post-Install Validation (mandatory)

Run this checklist before closing the installation:

- [ ] `AGENTS.md` exists and links to `docs/_index.md`
- [ ] `AGENTS.md` includes an authoritative directory tree
- [ ] `CLAUDE.md` contains the import `@AGENTS.md` (only Claude-Code-only instructions may follow it)
- [ ] `docs/_index.md` links to every created doc
- [ ] Every created doc has real content (no placeholders)
- [ ] Every created doc has at least 2 useful related links
- [ ] Every link is a standard relative Markdown link that resolves to an existing file
- [ ] Selected mode validation passed (`strict` or `adaptive`)
- [ ] Stable rules are inline in `AGENTS.md` → `## Stable Rules`
- [ ] `.claude/rules/coding-behavior-rules.md` exists and is linked from `AGENTS.md`
- [ ] `updating-docs` skill installed at `./.claude/skills/updating-docs/SKILL.md`
- [ ] `updating-docs` skill referenced by `AGENTS.md` Read First section
- [ ] `decisions.md` records key design choices
- [ ] Verification command for affected stack passed (`tsc --noEmit` for TypeScript repos)
- [ ] Work was committed in issue-scoped chunks
- [ ] `AGENTS.md` was updated at end of session
- [ ] Instruction-file migration coverage report included (if the repo had an `AGENTS.md` or legacy instruction files)
- [ ] Duplicate/valueless links were removed from `AGENTS.md` and `docs/`
- [ ] Cleanup decisions were human-approved item by item
- [ ] Link graph remains navigable and hub docs are still connected
- [ ] No low-signal doc sprawl or duplicate-topic docs were introduced
- [ ] Key docs include context/rationale where code alone is insufficient

---

## Troubleshooting & Edge Cases

### Repo has no clear structure
If the repo is a single-file project or lacks identifiable directories:
- Create a minimal doc tree: `AGENTS.md` + `CLAUDE.md` + `docs/_index.md` + `docs/project/overview.md`
- Skip categories that don't apply (no architecture doc if there's no architecture)

### Repo already has AGENTS.md
- It is the hub — read it first
- Preserve its content — merge it into the hub structure rather than overwriting, and move long sections into `docs/` behind a link
- Add the Stable Rules, Task Routing, Documentation Map, and Doc Workflow sections if missing
- Present the merge plan to the human for approval

### Repo already has CLAUDE.md
- Its content is a legacy source: map every meaningful section to `AGENTS.md` or `docs/` in Phase 2
- Replace its content with `@AGENTS.md` only after the Phase 3 migration coverage gate passes
- Instructions that apply to Claude Code alone stay in `CLAUDE.md`, below the import
- Present the migration plan to the human for approval

### Phase 1 analysis is incomplete
- Report what you could and could not determine
- Mark uncertain findings explicitly
- Proceed with what you know — the human can fill gaps during the approval step

### Repo uses a non-standard language/framework
- Identify entry points based on the framework's conventions
- Note the unfamiliar stack in your analysis
- Use the generic [PRINCIPLES.md](PRINCIPLES.md) guidelines — they apply to any stack

### Existing docs conflict with proposed structure
- Never delete existing docs without human approval
- Link existing docs from the new navigation hub
- Propose a migration plan in Phase 2

### Legacy instruction files exist but migration is incomplete
- Do NOT proceed to Phase 3 until every meaningful section of every legacy instruction file is mapped to a destination
- Use [TEMPLATES/migration-map.md](TEMPLATES/migration-map.md) to track section-level coverage
- Mark unknown or risky mappings explicitly and escalate to the human

---

## Related

- [README.md](README.md) — Project overview and usage guide
- [UPGRADE.md](UPGRADE.md) — Flow for repos that already have the v1 (`install-obsidian`) layout
- [PRINCIPLES.md](PRINCIPLES.md) — Design philosophy that governs all decisions
- [CONTRIBUTING.md](CONTRIBUTING.md) — How to contribute changes
- [CHANGELOG.md](CHANGELOG.md) — Version history
- [.claude/skills/updating-docs/SKILL.md](.claude/skills/updating-docs/SKILL.md) — Generic doc-update skill shipped with this installer

---

Start by reading [PRINCIPLES.md](PRINCIPLES.md), then [PHASES/01-analyze.md](PHASES/01-analyze.md).

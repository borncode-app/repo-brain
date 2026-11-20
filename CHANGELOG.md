# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed
- **BREAKING (contributor-facing):** `updating-docs` moved from `.claude/skills/updating-docs/` to `shipped/updating-docs/`. `npx skills add` walks `.claude/skills/`, so the skill was being offered to strangers as a standalone install even though it only makes sense inside an installed repo. It still installs to the target's `.claude/skills/updating-docs/` — only the source path in this repo changed. `PHASES/03-implement.md` step 3.6 now names both paths explicitly.
- AGENTS.md now carries the sections its own template requires: Identity, Task Routing, Working Rules, Doc Workflow, Documentation Map, Key Warnings

### Added
- `skills/repo-brain-install/SKILL.md` — the install as an agent skill. `npx skills add borncode-app/repo-brain --skill repo-brain-install` and "set up repo-brain in this repo" is enough; it routes to `AGENT-INSTALL.md` and the phases instead of restating them, and lists the fetch traps (summarizing fetch tools, no-network sandboxes) plus the gates a run must not skip
- AGENT-INSTALL.md — remote install entry point: an agent pointed at the GitHub URL resolves every relative installer link against `https://raw.githubusercontent.com/borncode-app/repo-brain/main/<path>`, fetches phases lazily, and copies the two shipped files from their raw URLs. Also records which agents fetch cleanly (Claude Code needs `curl` + `Read`, Codex CLI defaults to no network) and when to fall back to a shallow clone

### Changed
- README.md: "How to Use" (Option A clone / Option B feed phases) is replaced by three entry points — a paste-in prompt that needs no clone, `npx skills add` for agents that support skills, and a shallow clone when network is blocked — with a table for choosing between them
- PHASES/03-implement.md: distinguishes **entry-point skills** (`skills/<name>/`) from **shipped skills** (`.claude/skills/<name>/`); only shipped skills are copied to targets and must stay generic
- AGENTS.md: Rule Layers gains entry-point and installer-file rules; directory tree and Read First list both new entry points
- INSTALL.md: "Before You Start" gains a "Reached this file from a URL instead of a clone" subsection with the raw-base rule and the fetch-lazily rule
- UPGRADE.md: notes the raw-base rule for URL-reached runs

## [2.0.0] - 2026-11-17

Renamed from `install-obsidian` to `repo-brain`. Repos installed with 1.x: follow UPGRADE.md.

### Changed
- **BREAKING:** `AGENTS.md` is the hub and single source of truth, in this repo and in every target repo; `CLAUDE.md` holds one line, the import `@AGENTS.md`
- **BREAKING:** stable and security rules are written inline in `AGENTS.md` (`## Stable Rules`) instead of `.claude/rules/stable-rules.md` and `.claude/rules/security-rules.md`
- **BREAKING:** docs link with standard relative Markdown links instead of wiki-links; the dual format in Read With becomes one link whose text is the path from the repo root
- The installer's migration direction is reversed: an existing `AGENTS.md` is kept as the hub, and legacy instruction files (`CLAUDE.md` content, `.claude/rules/*`, other agent-specific files) are consolidated into it under the same section-level coverage gate. Before, `AGENTS.md` content was moved out and the file was offered for deletion
- PHASES/03-implement.md: step 3.4 creates `AGENTS.md`, step 3.5 ships `.claude/rules/coding-behavior-rules.md`, new step 3.9 points `CLAUDE.md` at `AGENTS.md`, and Final Verification moves to step 3.10
- TEMPLATES/hub-claude-md.md is renamed to TEMPLATES/hub-agents-md.md; the hub size guideline is now under 200 lines
- `updating-docs` skill reads `AGENTS.md` and teaches the relative-link convention
- README.md, INSTALL.md and PRINCIPLES.md treat Obsidian as an optional viewer instead of the target

### Added
- AGENTS.md — this repository's hub
- UPGRADE.md — upgrade flow for repos that have the 1.x layout
- INSTALL.md "Before You Start" and "One Hub for Every Agent" sections

### Removed
- .claude/rules/stable-rules.md and .claude/rules/security-rules.md — their rules moved into AGENTS.md

### Fixed
- PHASES/01-analyze.md: step 1.7 was swallowed by an unclosed code fence
- TEMPLATES hub template: nested code fences closed its Structure block early

### Repository maintenance
- History rewritten with `git filter-repo`: every commit's author and committer is now BornCode `<born113za@gmail.com>`, which GitHub resolves to the `borncode-app` account, so the Contributors graph lists a single contributor
- All `Co-authored-by` trailers removed from commit messages
- The 21 merged `copilot/*` branches were deleted; `main` and the annotated tag `v2.0.0` were force-pushed to the rewritten history
- File contents are byte-identical to the pre-rewrite tree

## [1.1.0] - 2026-06-05

_Versioned retroactively: these changes shipped on `main` after 1.0.0 without a release number._

### Added
- .claude/skills/updating-docs/SKILL.md — generic doc-update skill shipped to every target repo (read-first, write-second discipline, 6-item completion checklist, red flags)
- PHASES/03-implement.md step 3.6 — installer now copies the `updating-docs` skill to target's `.claude/skills/updating-docs/`
- TEMPLATES/migration-map.md — standard section-by-section migration map template for AGENTS.md and legacy docs
- INSTALL.md definition of done and mandatory post-install validation checklist
- CLAUDE.md — repository operational hub with directory tree, DoD, and session closeout
- .claude/rules/security-rules.md — stable security constraints separated from CLAUDE.md
- .claude/rules/stable-rules.md — stable project constraints separated from CLAUDE.md
- decisions.md — persistent design decision log for context resets
- PHASES/04-optimize-links.md — link-quality optimization for `CLAUDE.md` + `docs/`
- Hybrid strategy guidance across docs: preserve installer core and apply llm-wiki-inspired practices as a complementary layer
- Hybrid practicality gates and drift-guard checkpoints in installation workflow phases
- Template-level support for context/rationale capture and lightweight decision trace

### Changed
- INSTALL.md DoD now includes item 11 — `updating-docs` skill installed and referenced by `CLAUDE.md`
- INSTALL.md Post-Install Validation now includes two new checks for the skill
- INSTALL.md and README.md Core Outputs now list the `updating-docs` skill as a core deliverable in both modes
- TEMPLATES/hub-claude-md.md directory tree and Read First section now include `.claude/skills/updating-docs/`
- CLAUDE.md directory tree and Rule Layers now include the shipped skills folder
- INSTALL.md now requires installation mode selection (`strict` default or `adaptive`)
- README.md now documents strict vs adaptive output expectations
- PHASES/02-design.md now requires full AGENTS.md section mapping before Phase 3
- PHASES/03-implement.md now includes a 100% AGENTS.md migration coverage gate
- PHASES/05-cleanup.md now requires section-level migration evidence before deleting AGENTS.md
- TEMPLATES/hub-claude-md.md now requires stable rules in `./.claude/rules/`, directory tree, DoD, and session closeout
- INSTALL.md and PHASES/03-implement.md now include stable rules separation, decisions.md, and verification/closeout expectations
- INSTALL.md and README.md now include an Optimize Links phase for duplicate/valueless link cleanup
- Phase order now runs Optimize Links before Cleanup (Phase 4 then Phase 5)
- README.md now explicitly defines the hybrid model (`install-obsidian core` + `llm-wiki-inspired` layer)
- PRINCIPLES.md now adds hybrid doctrine and context/rationale-first anti-drift principles
- PHASES/01-05 now include systematic + flexible checkpoints and stronger anti-duplication guidance
- LICENSE now uses the MIT License

## [1.0.0] - 2026-04-18

### Added
- Initial release of install-obsidian instruction set
- INSTALL.md — step-by-step AI agent instructions
- PRINCIPLES.md — documentation design philosophy
- PHASES/ — four-phase execution workflow (Analyze, Design, Implement, Cleanup)
- TEMPLATES/ — document structure templates (architecture, feature, project, reference, index, hub-claude-md)
- README.md — project overview and usage guide
- LICENSE — Unlicense (public domain)
- .gitignore — OS and editor file exclusions
- CHANGELOG.md — version tracking
- CONTRIBUTING.md — contributor guidelines

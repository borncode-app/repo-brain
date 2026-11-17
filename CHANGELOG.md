# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

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

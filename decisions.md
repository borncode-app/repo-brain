# decisions.md

> Persistent design decisions for this repository.

## 2026-11-17 — Rewrite history so the Contributors graph shows one account

- **Decision**: rewrite every commit with `git filter-repo` so that author and committer are BornCode `<born113za@gmail.com>` — the address GitHub already resolves to the `borncode-app` account — and so that no commit message carries a `Co-authored-by` trailer. The 21 merged `copilot/*` branches were deleted, and `main` plus the annotated tag `v2.0.0` were force-pushed to the rewritten history.
- **Why**: the Contributors graph counted Copilot 24 and `borncode-app` 3. Copilot's 24 came from the *author* field of its commits, not from a trailer, so deleting trailers alone could not remove it. The remaining commits used two personal Gmail addresses that GitHub could not link to any account, so they were invisible in the graph. Rewriting the author field to the one address GitHub links makes every commit resolve to a single account.
- **Impact**: all 51 commit SHAs changed, so every clone must be reset rather than merged. File contents are byte-identical to the previous tree, which was verified before the push. The pre-rewrite history is kept as a local mirror at `C:\dev\repo-brain-backup.git` for the duration of the transition. The `/contributors` REST endpoint can still return the pre-rewrite numbers for a while; the `stats/contributors` endpoint that backs the `graphs/contributors` page already reports `borncode-app` alone.

## 2026-11-17 — Rename to repo-brain; `AGENTS.md` is the single source of truth

- **Decision**: rename the project from `install-obsidian` to `repo-brain`. The hub is `AGENTS.md`, in this repo and in every target repo. `CLAUDE.md` holds one line, the import `@AGENTS.md`. The `updating-docs` skill stays under `.claude/skills/`.
- **Why**: the knowledge base serves any agent, not one app. `AGENTS.md` is the instruction file agents share, while Claude Code reads `CLAUDE.md` and skips `AGENTS.md` whenever a `CLAUDE.md` exists — so a `CLAUDE.md` with content of its own would shadow the hub. The import was chosen over a symlink (on Windows, Git usually runs with `core.symlinks=false`, which checks a committed symlink out as a one-line text file) and over a sentence asking the agent to read `AGENTS.md` (nothing loads unless the agent decides to open the file). Skills stay in `.claude/skills/` because that is where Claude Code discovers them; `AGENTS.md` links the skill file so other agents can follow it as a plain procedure.
- **Impact**: the installer's migration direction is reversed. It used to move `AGENTS.md` content into `CLAUDE.md` + `docs/` and offer `AGENTS.md` for deletion; now an existing `AGENTS.md` is kept as the hub and legacy instruction files are consolidated into it. Earlier entries below that name `CLAUDE.md` as the hub now apply to `AGENTS.md`. Released as 2.0.0.

## 2026-11-17 — Stable rules live inline in `AGENTS.md`

- **Decision**: write stable and security rules in `AGENTS.md` under `## Stable Rules`, one line each. `coding-behavior-rules.md` stays a separate file in `.claude/rules/`, linked from that section. New rules for specific situations go under `docs/` with a Task Routing row. Supersedes "Separate stable rules from CLAUDE.md" (2026-04-21).
- **Why**: `.claude/rules/` is loaded by Claude Code only, so rules kept there never reached Codex, Cursor, or Copilot — the security rules included. `AGENTS.md` is the one file every agent loads at session start. The coding-behavior rules are 66 lines of guidance rather than constraints, so their four principles are named inline and the full text sits one link away, still auto-loaded by Claude Code.
- **Impact**: the overwrite risk behind the 2026-04-21 decision is now handled by a guard instead of a separate file: the section states that it changes only with human approval, and Session Closeout leaves it out of routine updates. The hub size guideline moves from 100 to 200 lines to make room.

## 2026-11-17 — Standard relative Markdown links replace wiki-links

- **Decision**: link docs as `[path/from/root.md](relative/href.md)`. The href is relative to the file containing the link and keeps `.md`; in navigation sections the link text is the target's path from the repo root. This replaces wiki-links and the dual format (backtick path plus wiki-link).
- **Why**: wiki-links render as plain text on GitHub and leave an agent guessing the path and extension, which is why the dual format existed. A standard link is navigable by agents, GitHub, editors, and Obsidian (its graph view and backlinks follow Markdown links too), so one link does both jobs.
- **Impact**: every template, phase, and the skill teach the new format, and Phase 4 rewrites any wiki-link it finds. Obsidian becomes an optional viewer.

## 2026-11-17 — Separate upgrade flow for repos installed with v1

- **Decision**: add `UPGRADE.md`, a focused flow that moves a v1 repo (hub in `CLAUDE.md`, rules in `.claude/rules/`, wiki-links) to the v2 layout without re-running analysis and design.
- **Why**: a v1 repo already has its docs tree, and its content-bearing `CLAUDE.md` would shadow a newly added `AGENTS.md`. The upgrade is a constrained migration — move the hub, inline the rules, convert the links, refresh the skill — so it lives in its own file instead of adding a branch to every phase.
- **Impact**: `INSTALL.md` routes v1 repos to `UPGRADE.md` before Phase 1. The upgrade reuses the migration-map template, the Post-Install Validation checklist, and the Phase 5 cleanup rules.

## 2026-06-05 — Ship generic `updating-docs` skill to every target repo

- **Decision**: add `.claude/skills/updating-docs/SKILL.md` to install-obsidian and have PHASES/03-implement step 3.6 copy it to the target repo's `.claude/skills/updating-docs/`. Treat the skill as a core output in both `strict` and `adaptive` modes.
- **Why**: docs in target repos drift (orphan docs, contradicted stable rules, raw paths instead of wiki links) when future agents skip context before writing. A pre-installed discipline skill forces read-first, write-second behavior so the doc graph stays navigable across sessions.
- **Impact**: the skill is generic (no install-obsidian-specific content) so it survives verbatim copy. INSTALL.md DoD, Post-Install Validation, and core outputs now include the skill. TEMPLATES/hub-claude-md.md and CLAUDE.md directory trees now include `.claude/skills/`.

## 2026-05-16 — Switch license to MIT

- **Decision**: replace the Unlicense with the MIT License.
- **Why**: align the project with the MIT licensing model.
- **Impact**: update LICENSE content and references in docs.

## 2026-05-16 — Run Optimize Links before Cleanup

- **Decision**: reorder phases so Optimize Links is Phase 4 and Cleanup is Phase 5.
- **Why**: align phase sequencing with the updated execution flow request.
- **Impact**: update phase file names and all references to match the new order.

## 2026-04-21 — Separate stable rules from CLAUDE.md

- **Decision**: keep immutable rules in `./.claude/rules/` and use `CLAUDE.md` as operational hub.
- **Why**: reduce accidental overwrite risk in session-level edits and prompt-driven changes.
- **Impact**: agents must read stable rules first, then apply session instructions.
- **Status**: superseded on 2026-11-17 — stable rules now live inline in `AGENTS.md`.

## 2026-04-21 — Keep an authoritative directory tree in CLAUDE.md

- **Decision**: include a repo tree snapshot in `CLAUDE.md`.
- **Why**: reduce path/structure misunderstanding across AI agents.
- **Impact**: update tree when structure changes.

## 2026-04-21 — Enforce explicit verification + session closeout

- **Decision**: add Definition of Done including `tsc --noEmit` for TypeScript repos and issue-scoped commits.
- **Why**: improve consistency and reduce regressions.
- **Impact**: agents must run verification and close every session with CLAUDE/decisions updates.

## 2026-04-23 — Adopt hybrid documentation strategy (core + inspired layer)

- **Decision**: preserve install-obsidian’s phase-based installer core, while adding llm-wiki-inspired practices as a complementary layer.
- **Why**: keep strong operational safeguards (approval gates, migration safety, stable rules) while improving retrieval quality via modular docs, better graph links, living updates, and rationale-first writing.
- **Impact**: README/INSTALL/PRINCIPLES/PHASES/TEMPLATES now enforce systematic-but-flexible behavior, drift prevention, and context-rich documentation expectations.

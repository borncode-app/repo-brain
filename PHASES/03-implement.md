# Phase 3: IMPLEMENT

> Create the documentation files approved in Phase 2.
> Follow the priority order from the approved design.

---

## Objective

Build the documentation system. Every file must have real content derived from repo analysis.

## Steps

### 3.1 Create Directory Structure

Create only the directories that were approved in Phase 2. Do NOT create categories that were not approved.

```bash
# Example — adjust to match the approved doc tree:
mkdir -p docs/project docs/architecture docs/features docs/reference
```

### 3.2 Create docs/_index.md

Use the [TEMPLATES/index-doc.md](../TEMPLATES/index-doc.md) pattern:
- Navigation hub with links to all docs
- Organized by category
- Include existing related files (README, etc.)

### 3.3 Create Docs in Priority Order

For each approved doc:

1. **Choose the right template** from [TEMPLATES/](../TEMPLATES/)
2. **Fill with real information** from your Phase 1 analysis
3. **Add links** to related docs — standard relative Markdown links ([PRINCIPLES.md](../PRINCIPLES.md), principle 5)
4. **Add Design Origin** if the feature has a spec/plan
5. **Add Related section** at the bottom
6. **Add context/rationale** where decisions are not obvious from code

Rules while writing:
- Every paragraph must contain information NOT obvious from the code
- Every doc must link to at least 2 other docs
- No doc should be a copy of something that already exists elsewhere
- Use the repo's actual terminology, not generic terms
- Keep each doc focused; split only when it improves retrieval and maintenance

### 3.4 Create AGENTS.md

Use [TEMPLATES/hub-agents-md.md](../TEMPLATES/hub-agents-md.md) as the structure guide:
- Keep it compact (under 200 lines)
- All links must point to real docs that exist
- Write `## Stable Rules` inline: security, compliance, and permanent constraints, one line each
- Working Rules must be specific to THIS repo
- Doc Workflow section must be included
- Include an authoritative directory tree
- If the repo already has an `AGENTS.md`, merge its content into this structure per the approved migration plan

### 3.5 Create decisions.md + Coding-Behavior Rules

Create or update:

1. `decisions.md` for design rationale that must survive context resets
2. `.claude/rules/coding-behavior-rules.md` — copy it verbatim from this installer repo (it is generic by design). Claude Code auto-loads it; every other agent reaches it through the link in `AGENTS.md` → `## Stable Rules`. If the target already has this file, keep the target's version.

Rules:
- decisions.md entries must include decision + rationale + impact
- Do not duplicate long explanations already covered in docs; link instead
- Any other rule goes in `AGENTS.md`: inline in `## Stable Rules` when it applies to every task, or as a doc under `docs/` with a Task Routing row when it applies to specific tasks

### 3.6 Install Updating-Docs Skill

The `updating-docs` skill ships with this installer. Copy it to the target repo so future agents can maintain docs without re-learning the discipline:

```bash
mkdir -p .claude/skills/updating-docs
```

1. Read the skill file from **this installer repo** at `shipped/updating-docs/SKILL.md`
2. Write it to **the target repo's** `.claude/skills/updating-docs/SKILL.md` (verbatim, no edits — the skill is generic by design)
3. Add a single line in the target's `AGENTS.md` "Read First" section linking `.claude/skills/updating-docs/SKILL.md` — Doc-update procedure (read-first, write-second discipline)
4. If the target already has a `.claude/skills/` folder, merge carefully — preserve any existing skills, append the new one

This is a **core output** in both `strict` and `adaptive` modes.

Source and destination differ, and the difference matters: it ships from `shipped/` in this repo and lands in `.claude/skills/` in the target. Only the target path is `.claude/skills/`, because that is where Claude Code discovers project skills; the link in the target's `AGENTS.md` lets every other agent follow the same file as a plain procedure. This repo keeps it outside `.claude/` so `npx skills add` does not offer it as an install for other repos.

#### Two Kinds of Skill in This Repo

| Kind | Location | Copied to targets? | May name `repo-brain`? |
|------|----------|--------------------|------------------------|
| **Shipped skill** | `shipped/<name>/SKILL.md` | Yes, verbatim → target's `.claude/skills/<name>/` | No — must stay generic |
| **Entry-point skill** | `skills/<name>/SKILL.md` | No, never | Yes — it is the installer's own front door |

`shipped/` and `skills/` are both outside `.claude/`, so `npx skills add` sees only `repo-brain-install`. A shipped
skill becomes a discoverable project skill only after it lands in the target's `.claude/skills/`.

`skills/repo-brain-install/SKILL.md` is the only entry-point skill. It routes an agent to
[AGENT-INSTALL.md](../AGENT-INSTALL.md) and the phase files instead of restating them, so the flow keeps one
source of truth. Install it from outside with `npx skills add borncode-app/repo-brain --skill repo-brain-install`.

#### Adding More Skills to the Installer

To ship an additional skill (e.g. `validating-docs`, `migrating-agents-md`):

1. Add the skill to this installer repo under `shipped/<skill-name>/SKILL.md`
   - Skill name uses kebab-case letters/numbers/hyphens only
   - Frontmatter: `name` + `description` (max 1024 chars; description starts with "Use when..." and lists triggers, not workflow)
2. Add a parallel step in this file (e.g. `3.7 Install <Skill-Name> Skill`) with the same copy-pattern as 3.6
3. Add a verification check in step 3.10 (Final Verification) for the new skill
4. Update `INSTALL.md` Definition of Done + Post-Install Validation with the new skill
5. Update `TEMPLATES/hub-agents-md.md` directory tree and Read First section
6. Update `README.md` Core Outputs + Folder Contents
7. Update `CHANGELOG.md` Unreleased → Added
8. Update `decisions.md` with the new design decision
9. Commit as a single issue-scoped change

**Rule of thumb:** keep each skill generic and self-contained. No skill should reference `repo-brain` or any other specific repo — that way it survives verbatim copy into arbitrary target repos.

### 3.7 Handle Existing Docs

Per the approved migration plan:
- Keep, redirect, or link existing docs as approved
- Do NOT delete anything the human hasn't explicitly approved for deletion
- If in doubt, preserve and link

### 3.8 Migration Coverage Gate (instruction files)

If the repo had an `AGENTS.md` or legacy instruction files:

1. Use the Phase 2 mapping table (or [TEMPLATES/migration-map.md](../TEMPLATES/migration-map.md)) as the source of truth
2. Verify each mapped section exists in its destination file/section
3. Produce a coverage summary:
   - `mapped sections: X/Y`
   - `verified migrated sections: X/Y`
   - `unmapped or uncertain sections: [list]`
4. Gate rule: coverage must be `Y/Y` (100%) before implementation can be considered complete
5. If any section is unmapped or uncertain, mark implementation as incomplete and return to migration work

### 3.9 Point CLAUDE.md at AGENTS.md

Run this step once the 3.8 gate passes, or right away when the repo had no instruction files to migrate.

1. Write `CLAUDE.md` in the repo root so that its first line is `@AGENTS.md`
2. Below the import, keep only the Claude-Code-only instructions the Phase 2 mapping marked `keep`; with none, the import is the whole file
3. Confirm `AGENTS.md` now holds everything the previous `CLAUDE.md` said to every agent

Write the import itself — a symlink breaks on Windows checkouts, and a sentence asking the agent to read `AGENTS.md` loads nothing by itself (see CLAUDE.md Companion in [TEMPLATES/hub-agents-md.md](../TEMPLATES/hub-agents-md.md)).

### 3.10 Final Verification

After creating all docs:

- [ ] Every doc has real content (no empty placeholders)
- [ ] Every link is a standard relative Markdown link that resolves to an existing file
- [ ] AGENTS.md links to every doc in the Documentation Map
- [ ] docs/_index.md links to every doc
- [ ] Every doc has a Related section with at least 2 links
- [ ] Every created doc (except hub and index) has a "## When to Read This" section
- [ ] Every "When to Read This" has both Trigger and Read With subsections
- [ ] Every Read With entry uses the format: `[docs/path/file.md](../path/file.md) — reason`
- [ ] Doc Workflow section exists in AGENTS.md
- [ ] AGENTS.md hub has a "## Task Routing" table derived from all Trigger sections
- [ ] Task Routing table links each real file, with the file path as the link text
- [ ] AGENTS.md contains an authoritative directory tree
- [ ] Stable rules are inline in AGENTS.md → `## Stable Rules`
- [ ] `CLAUDE.md` starts with the import `@AGENTS.md` and holds no instructions meant for other agents
- [ ] `.claude/rules/coding-behavior-rules.md` exists and is linked from AGENTS.md
- [ ] decisions.md exists and includes key design choices
- [ ] `updating-docs` skill installed at `.claude/skills/updating-docs/SKILL.md`
- [ ] `updating-docs` skill referenced in `AGENTS.md` "Read First"
- [ ] Verification commands passed for affected stack (`tsc --noEmit` for TypeScript repos)
- [ ] Work was committed in issue-scoped chunks
- [ ] AGENTS.md updated at end of session
- [ ] No hardcoded assumptions from other repos
- [ ] No information was lost from existing docs (if migration)
- [ ] Instruction-file migration coverage is 100% (if the repo had an AGENTS.md or legacy instruction files)
- [ ] Migration evidence includes section-level destinations (not only file-level)
- [ ] Each major doc includes context/rationale, not only file summaries
- [ ] No low-signal duplicate-topic docs were created
- [ ] Hybrid model check passed (installer core preserved + inspired layer applied)

---

## Output

Present the result:

```markdown
## Implementation Complete

### Created
- [list all new files, including AGENTS.md, CLAUDE.md, and .claude/skills/updating-docs/SKILL.md]

### Modified
- [list all changed files]

### Preserved
- [list untouched files]

### Verification
- [checklist results, including skill installation]

### Migration Coverage (if AGENTS.md or legacy instruction files existed)
- mapped sections: [X/Y]
- verified migrated sections: [X/Y]
- unresolved sections: [list or "none"]
```

Wait for the human's final review.

---

## Related

- [INSTALL.md](../INSTALL.md) — Main instruction flow
- [PRINCIPLES.md](../PRINCIPLES.md) — Design philosophy governing implementation
- [PHASES/02-design.md](02-design.md) — Previous phase: approved design
- [PHASES/04-optimize-links.md](04-optimize-links.md) — Next phase: optimize links
- [TEMPLATES/architecture-doc.md](../TEMPLATES/architecture-doc.md) — Architecture doc template
- [TEMPLATES/feature-doc.md](../TEMPLATES/feature-doc.md) — Feature doc template
- [TEMPLATES/project-doc.md](../TEMPLATES/project-doc.md) — Project doc template
- [TEMPLATES/reference-doc.md](../TEMPLATES/reference-doc.md) — Reference doc template
- [TEMPLATES/hub-agents-md.md](../TEMPLATES/hub-agents-md.md) — AGENTS.md hub template
- [TEMPLATES/index-doc.md](../TEMPLATES/index-doc.md) — Index doc template
- [TEMPLATES/migration-map.md](../TEMPLATES/migration-map.md) — Migration mapping template
- [shipped/updating-docs/SKILL.md](../shipped/updating-docs/SKILL.md) — Generic doc-update skill shipped with this installer

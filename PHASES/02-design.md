# Phase 2: DESIGN

> Propose a documentation tree tailored to this specific repo.
> Do NOT create any files yet. Only propose and wait for approval.

---

## Objective

Design the documentation architecture based on Phase 1 analysis.

## Steps

### 2.1 Propose Doc Tree

Based on the analysis, determine:

- Which category folders are justified (not every repo needs all categories)
- Which specific docs should exist (each must earn its existence per [PRINCIPLES.md](../PRINCIPLES.md))
- What AGENTS.md should contain

Present the proposed tree:

```markdown
## Proposed Doc Tree

repo-root/
├── AGENTS.md                  # [what it contains]
├── CLAUDE.md                  # one line: @AGENTS.md
├── docs/
│   ├── _index.md              # [what it contains]
│   ├── project/
│   │   └── <name>.md          # [why this doc exists]
│   ├── architecture/
│   │   └── <name>.md          # [why this doc exists]
│   └── ...
```

For each proposed doc, explain:
- **Why** it should exist (what gap it fills)
- **Source** of its content (which repo analysis finding it addresses)
- **Links** it should have (to which other docs)

### 2.2 Propose AGENTS.md Structure

Show the proposed sections of AGENTS.md:
- Identity
- Stable Rules (list each proposed rule, one line)
- Read First links
- Quick Commands
- Working Rules
- Documentation Map
- Key Warnings
- Doc Workflow

### 2.3 Migration Plan

If existing docs (README, older guides, etc.) have valuable information:
- Show which sections go where
- Show what stays unchanged
- Show what gets linked vs. rewritten
- Propose whether to keep, redirect, or remove existing docs

If the repo has an `AGENTS.md` or legacy instruction files (a `CLAUDE.md` with content, `.claude/rules/*`, other agent-specific instruction files), this mapping is mandatory and must be section-by-section.
Use [TEMPLATES/migration-map.md](../TEMPLATES/migration-map.md) and include every meaningful section.

Pick each section's destination:

| Source content | Destination | Method |
|----------------|-------------|--------|
| Rule that applies to every task | `AGENTS.md` → `## Stable Rules`, one line | rewrite |
| Operational guidance | The matching `AGENTS.md` section | rewrite |
| Long explanation or situational rule | A doc under `docs/`, reached from `AGENTS.md` Task Routing | rewrite |
| Instruction that applies to Claude Code alone | `CLAUDE.md`, below the import line | keep |
| `.claude/rules/` file the human wants Claude Code to keep auto-loading | Stays in place, linked from `AGENTS.md` | keep |

Required mapping table:

```markdown
### Instruction File Mapping (mandatory if AGENTS.md or legacy instruction files exist)
| Source file | Source section | Destination file | Destination section | Migration method (link/rewrite/keep) | Status |
|-------------|----------------|------------------|---------------------|----------------------------------------|--------|
| CLAUDE.md | [section name] | AGENTS.md | [heading] | rewrite | mapped |
```

Rules:
- Every meaningful section of every source file must appear in this table
- `Status` must be `mapped` for all rows before Phase 3
- If a section cannot be mapped, stop and request human guidance
- Do NOT proceed to [PHASES/03-implement.md](03-implement.md) with partial mapping
- When the repo has a `CLAUDE.md` with content, state in the proposal that Phase 3 replaces that content with the import `@AGENTS.md` once coverage is verified — the human's approval of the proposal authorizes the replacement

Include a **Files Marked for Removal** section:

```markdown
### Files Marked for Removal (pending Phase 5 verification)
| File | Content migrated to | Status |
|------|-------------------|--------|
| .claude/rules/stable-rules.md | `AGENTS.md` (Stable Rules) | proposed |
| old-doc.md | `docs/features/workflow.md` | proposed |
```

This list is used by Phase 5 to auto-detect and verify files eligible for cleanup.
Each file starts as `proposed` and gets verified during Phase 5.
`AGENTS.md` and `CLAUDE.md` never appear in this list: `AGENTS.md` is the hub, and `CLAUDE.md` is reduced to the import in Phase 3.

### 2.4 Priority Order

List docs in creation order (most useful first):

1. `[most critical doc]` — why first
2. `[second doc]` — why second
3. ...

### 2.5 Hybrid Fit Check (required)

Add a brief check before Phase 3:

- **Core preserved:** phase gates, stable rules in the hub, migration safeguards remain intact
- **Inspired layer applied:** docs are modular, linked, living, and context/rationale-driven
- **Drift guard:** no category/doc exists only because a template suggested it
- **Signal check:** proposed doc count is justified by repo complexity

---

## Output

Present your design as:

```markdown
## Design Proposal: [Repo Name]

### Proposed Doc Tree
[file tree with explanations]

### AGENTS.md Outline
[section structure, including the proposed Stable Rules]

### Migration Plan (if applicable)
[where existing info goes]

### Instruction File Migration Coverage
[100% required if AGENTS.md or legacy instruction files exist; otherwise "not applicable"]

### Priority Order
[creation sequence]

### Estimated Docs Count
[N docs to create]

### Hybrid Fit Check
[pass/fail + short rationale]
```

Wait for the human to approve or request changes before proceeding to [PHASES/03-implement.md](03-implement.md).

---

## Related

- [INSTALL.md](../INSTALL.md) — Main instruction flow
- [PRINCIPLES.md](../PRINCIPLES.md) — Design philosophy for doc tree decisions
- [PHASES/01-analyze.md](01-analyze.md) — Previous phase: repo analysis
- [PHASES/03-implement.md](03-implement.md) — Next phase: create the docs
- [TEMPLATES/hub-agents-md.md](../TEMPLATES/hub-agents-md.md) — Template for AGENTS.md hub
- [TEMPLATES/index-doc.md](../TEMPLATES/index-doc.md) — Template for docs/_index.md navigation
- [TEMPLATES/migration-map.md](../TEMPLATES/migration-map.md) — Template for section-by-section migration planning

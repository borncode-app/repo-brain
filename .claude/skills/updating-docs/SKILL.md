---
name: updating-docs
description: Use when user asks to update, add, or modify documentation in `docs/` of this repository, when creating a new feature/architecture/reference/project doc, when an agent is about to write in `docs/` and has not read `AGENTS.md` in the current session, or when docs are orphaned, contradict stable rules, or contain broken links. Triggers on "update docs", "document this", "add a doc for X", "เขียน docs", "อัพเดทเอกสาร".
---

# Updating Docs

## Overview

This skill enforces the **read-first, write-second** discipline for documentation work. The stable rules, the authoritative directory tree, and the Documentation Map all live in `AGENTS.md` — the hub every agent reads — and the link convention only works if every doc follows the pattern. Skipping context before writing creates orphan docs that future agents cannot find.

**Core principle:** Future agents must be able to navigate this repo from docs alone. Every doc is a memory cell — a disconnected doc is a lost memory.

## When to Use

- User says "update docs", "document this", "อัพเดทเอกสาร", "เขียน doc", "เพิ่ม doc"
- Creating a new feature/architecture/reference/project/integration/build/testing doc
- Modifying an existing doc and unsure of structure
- Touching `AGENTS.md` Documentation Map
- An agent is about to write in `docs/` and has not read `AGENTS.md` in this session

**Do NOT use for:**
- Inline code comments (use language conventions instead)
- `CHANGELOG.md` entries (use Keep a Changelog format)
- Decisions log (`decisions.md` has its own format)
- This repo's own governance files (top-level `README`, `INSTALL`, `PRINCIPLES`, `CONTRIBUTING`, `CHANGELOG`, `AGENTS.md`, `CLAUDE.md`) — those follow a different convention and are maintained outside this skill's scope, apart from the `AGENTS.md` Documentation Map and Task Routing rows this skill updates

## Required Pre-Reading (MUST do before writing)

**Iron Law: no doc written before these are read in this session.**

```bash
# 1. Project hub — Stable Rules (NON-NEGOTIABLE), directory tree, Task Routing, Documentation Map
Read AGENTS.md

# 2. Rule docs that AGENTS.md links for your topic
Read .claude/rules/coding-behavior-rules.md   # if doc is about coding workflow

# 3. Existing sibling doc — match its style, not invent a new one
Read docs/_index.md                       # see where your doc will live
Read the closest existing doc in the same category
```

**If you skip these, your doc will contradict a stable rule within 5 lines. This is not paranoia — it has happened.**

## The Workflow

```dot
digraph doc_workflow {
    "User asks to update/add doc" [shape=doublecircle];
    "Read AGENTS.md (hub + Stable Rules)" [shape=box];
    "Read existing sibling doc in same category" [shape=box];
    "Pick category" [shape=box];
    "Write doc following sibling structure" [shape=box];
    "Update docs/_index.md table" [shape=box];
    "Update AGENTS.md Documentation Map" [shape=box];
    "Verify >=2 links per doc, every link resolves" [shape=box];

    "User asks to update/add doc" -> "Read AGENTS.md (hub + Stable Rules)" [label="RED: must do first"];
    "Read AGENTS.md (hub + Stable Rules)" -> "Read existing sibling doc in same category";
    "Read existing sibling doc in same category" -> "Pick category";
    "Pick category" -> "Write doc following sibling structure";
    "Write doc following sibling structure" -> "Update docs/_index.md table";
    "Update docs/_index.md table" -> "Update AGENTS.md Documentation Map";
    "Update AGENTS.md Documentation Map" -> "Verify >=2 links per doc, every link resolves";
}
```

## Doc Category Decision

Where does this doc go? Match the existing repo's category set. The category that already has a similar doc is yours.

| Category | Path | When |
|----------|------|------|
| **Project** | `docs/project/` | Identity, stack, team roles — read first by every agent |
| **Feature workflow** | `docs/features/` | User-facing behavior, end-to-end business workflow |
| **Architecture** | `docs/architecture/` | Tech choices, schema, infra patterns, subsystem design |
| **Reference** | `docs/reference/` | Config, constants, conventions, design tokens |
| **Integration** | `docs/integrations/` | External tools, libraries, services |
| **Build** | `docs/build/` | Build, packaging, release |
| **Testing** | `docs/testing/` | Test strategy, conventions, fixtures |

**If unsure: read `docs/_index.md` table of contents. The category that already has a similar doc is yours. Do not create empty category folders — every room needs furniture.**

## Required Doc Structure

Match the template used by existing docs in this repo. A typical structure:

```markdown
# Title

> One-line description ending with period.

---

## Overview
What is this? 1-2 paragraphs.

## Context Snapshot
Bullets or table of the key facts a reader needs upfront.

## When to Read This
### Trigger
- Symptom or task that signals this doc applies.

### Read With
- [docs/path/file.md](../path/file.md) — reason

## [Main content sections...]
- Use H2 for major sections, H3 for sub-sections.
- Include code blocks for non-trivial examples.
- Cross-link to related docs with relative Markdown links (see Link Syntax below).

## Related
- [docs/path/related-1.md](../path/related-1.md) — why it's related
- [docs/path/related-2.md](../path/related-2.md) — why it's related
```

**Length guideline:** <500 words for most docs. If you need more, ask whether it should be split.

## The 6 Things You MUST Do (Checklist)

After writing the doc, verify ALL of these:

- [ ] **1. Links**: Doc has >= 2 relative Markdown links to other docs, and every link resolves to an existing file
- [ ] **2. `_index.md` updated**: New row added in the correct category table
- [ ] **3. `AGENTS.md` Documentation Map updated**: New row added under the right heading
- [ ] **4. `AGENTS.md` Task Routing updated** (if the doc adds a new "if you are working on X → read Y" path)
- [ ] **5. Language**: Match the repo's content language for user-facing examples, English for code/config (per stable rules)
- [ ] **6. No contradictions with `AGENTS.md` Stable Rules**: Re-read them before declaring done

**If any item unchecked, the doc is not done.** The user will assume you did all 6.

## Common Failures and Fixes

| Failure | Why it happens | Fix |
|---------|----------------|-----|
| Doc not findable from `_index.md` | Agent forgot index step | Always include the index update in your workflow — it is part of "the doc" |
| Doc contradicts a stable rule | Agent skipped pre-reading | Re-read rules — pre-reading is iron law, no exceptions |
| Doc uses a `[[wiki-link]]` or a bare path | Agent did not know the link convention | Use a relative Markdown link — `[docs/features/X.md](../features/X.md)` — it resolves for agents, on GitHub, and in Obsidian |
| Orphan doc, no related links | Agent stopped after writing the doc | Section "## Related" is mandatory, not optional |
| Doc explains things obvious from code | Agent over-explained | Match sibling doc depth; if sibling has 50 lines, yours should not have 500 |
| One doc per folder regardless of value | Agent over-applied category rule | Categories are rooms, not slots — skip empty rooms |
| Doc duplicates content from AGENTS.md | Agent did not check the hub first | Link to AGENTS.md instead of rewriting |
| Doc has 3 paragraphs of "history of how we got here" | Agent wrote narrative | Cut to Overview + Context Snapshot — narrative goes in commits |

## Red Flags — STOP and Restart

If you catch yourself doing any of these, delete the doc and start over:

- "I will add the cross-links later" — they will be forgotten
- "The user only asked for the doc, not the index" — index update is part of "the doc"
- "I already know the rules, no need to re-read" — that is exactly when you miss them
- "It is a small doc, does not need structure" — small docs benefit from structure MORE, not less
- "The doc is fine without Related section" — orphan docs are useless docs
- "I will just write it quickly, fix structure after" — you will never fix it after
- "This doc is unrelated to the rules" — every doc is downstream of stable rules
- "Skipping _index.md because it is just navigation" — navigation IS the point

**All of these mean: delete what you wrote, re-read the rules, and start over following the workflow.**

## Quick Reference: Link Syntax

The href is relative to the file you are editing and keeps the `.md` extension. In navigation sections (Read With, Related, `docs/_index.md`, the Documentation Map) the link text is the target's path from the repo root.

```markdown
# GOOD — standard relative Markdown link
[docs/features/X.md](../features/X.md)      # written in docs/architecture/
[docs/features/X.md](X.md)                  # written in docs/features/
[docs/features/X.md](features/X.md)         # written in docs/_index.md
[docs/features/X.md](docs/features/X.md)    # written in AGENTS.md (repo root)

# BAD — not a working link on GitHub or for agents
[[docs/features/X]]
docs/features/X.md
```

## Quick Reference: When to Read Which Rule

| Rule source | Read before docs that touch... |
|-------------|-------------------------------|
| `AGENTS.md` → Stable Rules | Always |
| `.claude/rules/coding-behavior-rules.md` | Docs about coding workflow, TDD, surgical changes |
| Any other rule doc linked from `AGENTS.md` | The topic that rule doc covers |

## Real Example: Adding a New Feature Doc

**User:** "Document the new feature X"

**Step 1 — Read (RED phase):**
```bash
Read AGENTS.md
Read docs/_index.md
Read docs/features/closest-sibling.md
```

**Step 2 — Decide category:** Feature → `docs/features/X.md`

**Step 3 — Write** following the sibling's template.

**Step 4 — Update both maps:**
- `docs/_index.md` → add row in "Features" table
- `AGENTS.md` → add row in Documentation Map "Features" section

**Step 5 — Cross-link:** `[docs/features/closest-sibling.md](closest-sibling.md)`, `[docs/architecture/tech-stack.md](../architecture/tech-stack.md)`

**Step 6 — Verify:** Run through the 6-item checklist above.

## Related

- `AGENTS.md` — Project hub: Stable Rules, directory tree, Task Routing, and the Documentation Map
- `docs/_index.md` — Documentation index you must update when adding a doc
- `TEMPLATES/*` in this repo (if present) — doc structure templates; match your new doc to the closest existing sibling
- `docs/features/<closest-sibling>` — the most similar existing doc in the same category; match its style

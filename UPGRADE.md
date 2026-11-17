# UPGRADE — Move a v1 Repo to repo-brain v2

> For repos that already ran the v1 installer (`install-obsidian`).
> For any other repo, use [INSTALL.md](INSTALL.md).

---

## When This Applies

The repo has the v1 layout when `CLAUDE.md` holds a `## Documentation Map` and `docs/_index.md` exists.

## What Changes

| Area | v1 layout | v2 layout |
|------|-----------|-----------|
| Hub | `CLAUDE.md` | `AGENTS.md`, same sections |
| `CLAUDE.md` | Hub content | One line: `@AGENTS.md` |
| Rules that apply to every task | `.claude/rules/stable-rules.md`, `.claude/rules/security-rules.md` | Inline in `AGENTS.md` → `## Stable Rules` |
| Other files in `.claude/rules/` | Linked from `CLAUDE.md` | Stay in place, linked from `AGENTS.md` |
| Links | `[[wiki-links]]`, dual format in Read With | Standard relative Markdown links |
| `updating-docs` skill | v1 text | v2 text |
| `docs/` content, `decisions.md` | — | Unchanged apart from links |

Why the hub moves instead of being copied: `AGENTS.md` is the one instruction file every agent loads, while rules stored only under `.claude/rules/` reach Claude Code alone. A `CLAUDE.md` with content of its own makes Claude Code read it instead of `AGENTS.md`, so two hubs would drift apart.

The docs tree keeps its structure. This upgrade moves the hub and rewrites links; doc content stays as written.

## Steps

Run in order. Each step ends when its **Done when** line is true.

### U1 Start From a Clean State

Run `git status`. If there are pending changes, ask the human to commit or stash them. Work on a branch unless the repo's own workflow says otherwise.

**Done when:** the working tree is clean before your first edit.

### U2 Map Every Section (no file changes)

Build a migration map with [TEMPLATES/migration-map.md](TEMPLATES/migration-map.md). Source files: `CLAUDE.md`, every file under `.claude/rules/`, and `AGENTS.md` if one already exists.

| Source | Destination | Method |
|--------|-------------|--------|
| `CLAUDE.md` section | The same section in `AGENTS.md` | rewrite |
| `CLAUDE.md` instruction that applies to Claude Code alone | `CLAUDE.md`, below the import | keep |
| Each rule in `stable-rules.md` and `security-rules.md` | One line in `AGENTS.md` → `## Stable Rules` | rewrite |
| Explanation too long for one line | A doc under `docs/`, linked from the rule's line | rewrite |
| Any other `.claude/rules/` file | Stays in place and gets a link in `AGENTS.md`: under Stable Rules for always-on guidance, in Task Routing for situational rules | keep |

Present the map and the list of files you will change. Wait for the human's approval.

**Done when:** every section of `CLAUDE.md` and every rule under `.claude/rules/` has a row with status `mapped`, and the human approved the map.

### U3 Build AGENTS.md

Create `AGENTS.md` from [TEMPLATES/hub-agents-md.md](TEMPLATES/hub-agents-md.md), filling each section from the map. Carry rule wording over exactly.

**Done when:** every row of the map is `verified` against `AGENTS.md` or its `docs/` destination — coverage `Y/Y`.

### U4 Point CLAUDE.md at AGENTS.md

Replace the content of `CLAUDE.md` with the import line `@AGENTS.md`, followed only by the instructions the map marked `keep`.

**Done when:** `CLAUDE.md` starts with `@AGENTS.md` and holds nothing meant for other agents.

### U5 Convert Links

In `AGENTS.md`, `docs/**/*.md`, `decisions.md`, and every other Markdown file that links docs, rewrite each link to the v2 convention ([PRINCIPLES.md](PRINCIPLES.md), principle 5). The hrefs below are for a file inside `docs/architecture/`; compute each href relative to the file you are editing.

```text
[[docs/features/x]]                                →  [docs/features/x.md](../features/x.md)
[[docs/features/x|label]]                          →  [label](../features/x.md)
[[docs/features/x#Heading]]                        →  [docs/features/x.md](../features/x.md#heading)
`docs/features/x.md` [[docs/features/x]] — reason  →  [docs/features/x.md](../features/x.md) — reason
[[x]]  (short name)                                →  find the one file it means; ask the human when several match
```

- Convert links only. Inside code blocks and inline code, `[[` is usually shell syntax and stays as written.
- Every `CLAUDE.md` mention that means "the hub" becomes `AGENTS.md`.

**Done when:** a search for `[[` in those files finds matches only inside code, and every relative link resolves to an existing file.

### U6 Refresh the Skill

Replace `.claude/skills/updating-docs/SKILL.md` with the file from this installer. List every other skill or rule file that names `CLAUDE.md` as the hub, points at `.claude/rules/stable-rules.md`, or teaches wiki-link syntax, and update those references once the human agrees.

**Done when:** no file under `.claude/` describes `CLAUDE.md` as the hub or wiki-links as the convention.

### U7 Verify and Record

1. Run the Post-Install Validation checklist in [INSTALL.md](INSTALL.md)
2. Add a `decisions.md` entry: the hub moved to `AGENTS.md`, the stable rules moved inline, the links were converted
3. Report the line count of `AGENTS.md`; above 200 lines, list the sections that could move to `docs/` and leave that for a separate change

**Done when:** every checklist item passes, or is reported to the human with its reason.

### U8 Clean Up (human-approved)

Follow steps 5.3–5.6 of [PHASES/05-cleanup.md](PHASES/05-cleanup.md) for `.claude/rules/stable-rules.md`, `.claude/rules/security-rules.md`, and any other file whose content the map moved.

**Done when:** each candidate is deleted or kept according to the human's individual answer, and no link points at a deleted file.

---

## Related

- [INSTALL.md](INSTALL.md) — Fresh-install flow and the Post-Install Validation checklist
- [PRINCIPLES.md](PRINCIPLES.md) — Link convention and hub rules
- [TEMPLATES/hub-agents-md.md](TEMPLATES/hub-agents-md.md) — AGENTS.md structure and the CLAUDE.md companion
- [TEMPLATES/migration-map.md](TEMPLATES/migration-map.md) — Section-level migration map
- [PHASES/05-cleanup.md](PHASES/05-cleanup.md) — Cleanup rules
- [decisions.md](decisions.md) — Why v2 changed the hub, the rules, and the links

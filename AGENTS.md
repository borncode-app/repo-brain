# repo-brain — Project Hub

> Single source of truth for AI agents working in this repository. Every agent reads this file first.
> `CLAUDE.md` contains only the import `@AGENTS.md`, so Claude Code loads this same file.

---

## Identity

| Field | Value |
|-------|-------|
| Name | repo-brain |
| Type | Installer — Markdown instruction set, no code |
| Stack | Markdown only (`INSTALL.md` + `PHASES/` + `TEMPLATES/` + skills) |
| Version | 2.0.0 |
| Repo | https://github.com/borncode-app/repo-brain |
| Formerly | `install-obsidian` (v1) |

---

## Stable Rules

> Non-negotiable. They apply to every task and every agent, and task-level prompts do not relax them.
> Change this section only with explicit human approval.

### Project

1. Keep instructions AI-agent-friendly: clear, sequential, unambiguous.
2. Prefer small, focused edits over broad rewrites.
3. Do not create empty placeholder docs.
4. Avoid duplicating information; use links instead.
5. Keep templates generic (no repo-specific assumptions).
6. Maintain changelog entries for notable behavioral/instruction changes.

### Security

1. Never commit credentials, tokens, private keys, or secrets.
2. Never exfiltrate repository code/content to third-party systems.
3. Do not introduce new security vulnerabilities when changing files.
4. Validate security impact for modified areas before finalizing.
5. If a requested action conflicts with security policy, stop and escalate.

### Coding behavior

Think before coding, simplicity first, surgical changes, goal-driven execution. Read the full text before changing any file: [.claude/rules/coding-behavior-rules.md](.claude/rules/coding-behavior-rules.md).

---

## Read First

- [README.md](README.md) — project overview
- [AGENT-INSTALL.md](AGENT-INSTALL.md) — remote install entry point (how an agent reaches the installer from a URL)
- [skills/repo-brain-install/SKILL.md](skills/repo-brain-install/SKILL.md) — the same install as an installable skill
- [INSTALL.md](INSTALL.md) — execution flow for AI agents (fresh install)
- [UPGRADE.md](UPGRADE.md) — execution flow for repos installed with v1 (`install-obsidian`)
- [PRINCIPLES.md](PRINCIPLES.md) — design rules
- [shipped/updating-docs/SKILL.md](shipped/updating-docs/SKILL.md) — generic doc-update skill shipped to target repos (read this when working on the skill itself or Phase 3 step 3.6)

---

## Task Routing

> If you are working on X → read Y first.

| Task | Read First |
|------|------------|
| Changing the install flow, phases, or gates | [INSTALL.md](INSTALL.md), then the phase file you touch |
| Changing how an agent reaches the installer | [AGENT-INSTALL.md](AGENT-INSTALL.md) |
| Changing the installable skill | [skills/repo-brain-install/SKILL.md](skills/repo-brain-install/SKILL.md) |
| Changing the shipped doc-update skill | [shipped/updating-docs/SKILL.md](shipped/updating-docs/SKILL.md), then step 3.6 in [PHASES/03-implement.md](PHASES/03-implement.md) |
| Adding or changing a template | [TEMPLATES/hub-agents-md.md](TEMPLATES/hub-agents-md.md) and its neighbors |
| Upgrading a v1 (`install-obsidian`) repo | [UPGRADE.md](UPGRADE.md) |
| Changing design rules the installer applies | [PRINCIPLES.md](PRINCIPLES.md) |

---

## Working Rules

1. **Markdown only** — this repo has no code, no build, and no tests. Verification means checking links, fences, and paths.
2. **The flow has one home** — `INSTALL.md` and `PHASES/` own the steps. Entry points route to them; they never restate them (Rule Layers 7).
3. **Shipped files stay generic** — `shipped/updating-docs/SKILL.md` and `.claude/rules/coding-behavior-rules.md` are copied verbatim into other repos, so neither may name `repo-brain`.
4. **Entry points match the flow** — a phase change means checking `AGENT-INSTALL.md` and the skill still point at real files.
5. **Verify a skill move with the CLI** — `npx skills add . --list` must find exactly the entry-point skills, never a shipped one.
6. **Do not add a `docs/` tree here** — this repo is the installer, not an installed repo. `docs/` belongs to targets.

---

## Doc Workflow

This repo does not use a `docs/` tree. Knowledge lives in the top-level files, and each has one job:

| Change | Goes to |
|--------|---------|
| A lasting design decision | [decisions.md](decisions.md) — decision, why, impact |
| A user-visible or behavioral change | [CHANGELOG.md](CHANGELOG.md) under `[Unreleased]` |
| A new install rule or gate | [INSTALL.md](INSTALL.md) or the relevant `PHASES/` file |
| A new doc structure | `TEMPLATES/` |
| A change to how agents find repo-brain | [AGENT-INSTALL.md](AGENT-INSTALL.md) or `skills/repo-brain-install/` |

After any change, confirm links resolve and the page still reads correctly from the top.

---

## Documentation Map

- [README.md](README.md) — user-facing entry point and the three install methods
- [AGENT-INSTALL.md](AGENT-INSTALL.md) — remote install entry point for agents
- [skills/repo-brain-install/SKILL.md](skills/repo-brain-install/SKILL.md) — the install as an installable skill
- [INSTALL.md](INSTALL.md) — the flow: phases, modes, gates, validation
- [UPGRADE.md](UPGRADE.md) — v1 (`install-obsidian`) upgrade flow
- [PRINCIPLES.md](PRINCIPLES.md) — design rules every phase follows
- [CONTRIBUTING.md](CONTRIBUTING.md) — contributor guidelines
- [CHANGELOG.md](CHANGELOG.md) — version history
- [decisions.md](decisions.md) — persistent design decisions
- [shipped/updating-docs/SKILL.md](shipped/updating-docs/SKILL.md) — doc-update skill shipped to targets

---

## Key Warnings

- **`CLAUDE.md` must stay one line** — `@AGENTS.md`. Content of its own makes Claude Code read it instead of this hub, and the two drift apart.
- **Moving a shipped file breaks the installer** — `PHASES/03-implement.md` steps 3.5 and 3.6 name the exact source paths. Update them in the same change.
- **`npx skills add` walks `.claude/skills/`** — anything placed there becomes installable by strangers. Shipped skills belong in `shipped/`.
- **Templates are structure, not content** — filling them in with repo-brain's own details would make them useless for target repos.

---

## Directory Tree (Authoritative)

```text
repo-brain/
├── .claude/
│   └── rules/
│       └── coding-behavior-rules.md
├── PHASES/
├── TEMPLATES/
├── shipped/
│   └── updating-docs/
│       └── SKILL.md
├── skills/
│   └── repo-brain-install/
│       └── SKILL.md
├── AGENT-INSTALL.md
├── AGENTS.md
├── CHANGELOG.md
├── CLAUDE.md
├── CONTRIBUTING.md
├── INSTALL.md
├── LICENSE
├── PRINCIPLES.md
├── README.md
├── UPGRADE.md
└── decisions.md
```

---

## Rule Layers

1. **Stable rules (immutable)**: the `## Stable Rules` section above — project rules, security rules, and the Karpathy-inspired coding-behavior rules it links to.
2. **Operational rules (editable)**: the rest of this `AGENTS.md`, for workflow/navigation.
3. **Task-specific instructions**: follow user instructions in current session.
4. **Hybrid strategy**: preserve installer core requirements; apply llm-wiki-inspired practices as a complementary layer.
5. **Shipped files**: the installer copies `.claude/rules/coding-behavior-rules.md` and `shipped/updating-docs/SKILL.md` verbatim to every target repo (see [PHASES/03-implement.md](PHASES/03-implement.md) steps 3.5 and 3.6), so both must stay generic. `shipped/` sits outside `.claude/` so `npx skills add` never offers it as a standalone install.
6. **Entry-point files**: `AGENT-INSTALL.md` and `skills/repo-brain-install/SKILL.md` are the installer's own front doors. They may name `repo-brain` and its URLs; nothing under `.claude/` may, and they are never copied into a target repo.
7. **Installer files**: `INSTALL.md`, `UPGRADE.md`, `PHASES/`, and `TEMPLATES/` stay the single source of truth for the flow. The entry-point files route to them and must not restate the steps.

---

## Definition of Done (Session)

- [ ] Requested change is implemented with minimal scope.
- [ ] Related docs/instructions are updated when behavior changed.
- [ ] Verification commands were run for affected stack:
  - TypeScript: `tsc --noEmit`
  - Otherwise: run equivalent existing validation commands in repo
- [ ] Commit is scoped to one issue/change set.
- [ ] `decisions.md` updated when design/strategy decisions were made.
- [ ] `AGENTS.md` reviewed and updated to reflect current project state.

---

## Session Closeout

At the end of every session, run a final pass:

1. Update `AGENTS.md` to match current project state (`## Stable Rules` changes only with human approval)
2. Update `decisions.md` for any new lasting decisions
3. Confirm links and paths still point to existing files

---

## Related

- [AGENT-INSTALL.md](AGENT-INSTALL.md)
- [INSTALL.md](INSTALL.md)
- [UPGRADE.md](UPGRADE.md)
- [PRINCIPLES.md](PRINCIPLES.md)
- [CHANGELOG.md](CHANGELOG.md)
- [decisions.md](decisions.md)

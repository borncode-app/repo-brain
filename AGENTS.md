# repo-brain — Project Hub

> Single source of truth for AI agents working in this repository. Every agent reads this file first.
> `CLAUDE.md` contains only the import `@AGENTS.md`, so Claude Code loads this same file.

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
- [.claude/skills/updating-docs/SKILL.md](.claude/skills/updating-docs/SKILL.md) — generic doc-update skill shipped to target repos (read this when working on the skill itself or Phase 3 step 3.6)

---

## Directory Tree (Authoritative)

```text
repo-brain/
├── .claude/
│   ├── rules/
│   │   └── coding-behavior-rules.md
│   └── skills/
│       └── updating-docs/
│           └── SKILL.md
├── PHASES/
├── skills/
│   └── repo-brain-install/
│       └── SKILL.md
├── TEMPLATES/
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
5. **Shipped files**: the installer copies `.claude/rules/coding-behavior-rules.md` and `.claude/skills/updating-docs/SKILL.md` verbatim to every target repo (see [PHASES/03-implement.md](PHASES/03-implement.md) steps 3.5 and 3.6), so both must stay generic.
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

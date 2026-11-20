# repo-brain

> Give any repository a brain that every AI agent can read.
> Drop this folder into any repo. AI reads the instructions, analyzes your codebase, and builds a linked knowledge base with `AGENTS.md` as its single source of truth.

![Version](https://img.shields.io/badge/version-2.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)

Formerly `install-obsidian`.

---

## What This Does

This is **not** a traditional installer. It is a set of Markdown instructions that AI agents (Claude Code, Codex, Copilot, Cursor, etc.) read to:

1. **Analyze** your repo structure
2. **Design** a documentation tree tailored to your codebase
3. **Create** interconnected Markdown docs behind one hub, `AGENTS.md`
4. **Optimize** link structure to remove duplicate/valueless links for cleaner graph + lower token use

The result: your repo gains a living knowledge base that both humans and AI can navigate.

## One Brain for Every Agent

- **`AGENTS.md` is the single source of truth.** It is the instruction file agents share — Codex, Cursor, GitHub Copilot, and [many others](https://agents.md) read it directly.
- **`CLAUDE.md` is one line: `@AGENTS.md`.** Claude Code expands the import at session start and loads the same hub. The import works on every platform; a symlink turns into a one-line text file on a default Windows checkout, and a sentence saying "read AGENTS.md" loads nothing by itself.
- **Stable rules live inline in `AGENTS.md`.** Rules kept in an agent-specific folder reach only that agent.
- **Links are standard relative Markdown links.** They resolve for agents, on GitHub, in editors, and in Obsidian.

## Hybrid Strategy (Core + Inspired Layer)

This project uses a **hybrid** approach:

- **Core (repo-brain installer, non-negotiable):** phase-based installer flow, stable rules, migration safety, and practical completion gates
- **Inspired layer (llm-wiki style):** smaller knowledge units, high-signal cross-links, living docs, and rationale-first writing

The inspired layer is an enhancement, not a replacement for the installer core.

## Install

Pick **one** of the three methods below. They are alternatives, not steps — each one installs the same thing, so
you never run more than one.

### Method 1 — Paste this into any agent (recommended)

```text
Install repo-brain in this repo: read
https://raw.githubusercontent.com/borncode-app/repo-brain/main/AGENT-INSTALL.md
and follow it end to end. Ask me before you change anything.
```

### Method 2 — Install the skill, then just ask

If your agent supports [skills](https://agentskills.io) and you have Node.js 22.20+, install the skill once. After
that, "set up repo-brain in this repo" is enough — no URL to paste.

```bash
npx skills add borncode-app/repo-brain --skill repo-brain-install
```

Then, in any repo:

```text
Set up repo-brain in this repo.
```

The skill also works with `-g` for all projects, `-a claude-code` to skip the agent picker, and
`npx skills update` to keep it current.

### Method 3 — Clone, when your agent has no network

```bash
git clone --depth 1 https://github.com/borncode-app/repo-brain.git /tmp/repo-brain
```

```text
Read /tmp/repo-brain/INSTALL.md and follow it end to end.
```

Whichever you pick, the agent analyzes your codebase, proposes a doc tree, and builds it after you approve. It
confirms two things as it goes: which repo it is installing into, and whether you want `strict` (default, full
structure) or `adaptive` (only the categories your repo justifies).

There is no package, no build step, and nothing added to your `package.json`. The outputs are listed under
[What You Get](#what-you-get).

### Which method should I pick?

| Situation | Use |
|-----------|-----|
| Any agent, one time | Method 1 — the paste-in prompt |
| You will use repo-brain on several repos | Method 2 — install the skill once |
| Network is blocked, or you want the files locally | Method 3 — clone |

[AGENT-INSTALL.md](AGENT-INSTALL.md) lists which agents fetch cleanly and which need Method 3.

### Upgrading a repo installed with install-obsidian (v1)

If your `CLAUDE.md` is the hub and your docs use `[[wiki-links]]`, run this instead:

```text
Upgrade this repo to repo-brain v2: read
https://raw.githubusercontent.com/borncode-app/repo-brain/main/UPGRADE.md
and follow it end to end.
```

The skill handles this too: if you installed it, say "upgrade this repo to repo-brain v2".

### Reading it yourself

The repo page is the whole installer: [INSTALL.md](INSTALL.md) is the flow,
[PHASES/01-analyze.md](PHASES/01-analyze.md) through [PHASES/05-cleanup.md](PHASES/05-cleanup.md) are the steps,
[TEMPLATES/hub-agents-md.md](TEMPLATES/hub-agents-md.md) and its neighbors are the structures. Each phase
documents its own output and its own gate.

## What You Get

This installer supports two output modes.

### Core outputs in both modes

- `AGENTS.md` as the project hub — the single source of truth every agent reads first, with the stable rules inline
- `CLAUDE.md` holding one line, `@AGENTS.md`, so Claude Code loads the same hub
- `docs/_index.md` as the documentation navigation hub
- `./.claude/rules/coding-behavior-rules.md` — coding-behavior guidelines, linked from `AGENTS.md`
- `./.claude/skills/updating-docs/SKILL.md` — generic doc-update skill (forces read-first, write-second discipline for future agents)
- `decisions.md` for persistent design decisions across sessions

### Strict mode (default)

Creates a full standardized documentation skeleton:

```
your-repo/
├── AGENTS.md              # Project hub (every agent reads this first)
├── CLAUDE.md              # One line: @AGENTS.md
├── docs/
│   ├── _index.md          # Documentation navigation hub
│   ├── project/           # Project-level knowledge
│   ├── architecture/      # Structure and subsystem docs
│   ├── features/          # Feature workflow docs
│   ├── integrations/      # External dependency docs (if applicable)
│   ├── build/             # Build/packaging docs (if applicable)
│   ├── testing/           # Testing knowledge
│   └── reference/         # Stable reference docs
```

### Adaptive mode

Creates only categories justified by repo analysis (example):

```
your-repo/
├── AGENTS.md
├── CLAUDE.md
├── docs/
│   ├── _index.md
│   ├── project/
│   ├── architecture/
│   └── features/
```

In both modes, files must contain real content. No empty placeholders.

## Philosophy

- **Flex, not static** — AI analyzes YOUR repo, creates docs that match YOUR structure
- **Hub-and-spoke** — AGENTS.md is the front door, docs/ are the rooms
- **Graph-friendly** — standard relative links between docs work for agents, on GitHub, and in Obsidian graph view
- **Minimal** — Only creates docs where real knowledge exists, no empty placeholders
- **Context-first** — explain why decisions and workflows exist, not only where files are

## Folder Contents

| File | Purpose |
|------|---------|
| [AGENT-INSTALL.md](AGENT-INSTALL.md) | Remote install entry point: how an agent reaches the installer from a URL |
| [skills/repo-brain-install/SKILL.md](skills/repo-brain-install/SKILL.md) | The same install as an installable agent skill (`npx skills add`) |
| [INSTALL.md](INSTALL.md) | Step-by-step instructions for AI agents |
| [UPGRADE.md](UPGRADE.md) | Upgrade flow for repos installed with v1 (`install-obsidian`) |
| [PRINCIPLES.md](PRINCIPLES.md) | Design principles and decision framework |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contributor guidelines |
| [CHANGELOG.md](CHANGELOG.md) | Version tracking |
| `AGENTS.md` | Operational hub used by AI agents working on this repo |
| `CLAUDE.md` | One-line import of `AGENTS.md` for Claude Code |
| `decisions.md` | Persistent design decision log |
| `.claude/rules/` | Coding-behavior rules shipped to target repos |
| `shipped/` | Skills shipped to target repos (`updating-docs`) |
| `TEMPLATES/` | Document structure templates, including migration mapping |
| `PHASES/` | Sequential execution phases (Analyze → Design → Implement → Optimize Links → Cleanup) |

## After Installation

The knowledge base is plain Markdown with standard relative links, so it works wherever Markdown does.

1. Start a new agent session — it loads `AGENTS.md` (Claude Code through `CLAUDE.md`)
2. When you add new features, AI will follow the Doc Workflow in AGENTS.md to create new docs automatically

Optional — browse the docs as a graph in Obsidian:

1. Open your repo folder as a vault
2. In Settings > Files & Links, turn off "Use [[Wikilinks]]" and set "New link format" to "Relative path to file", so links you create in Obsidian follow the same convention
3. Open graph view to see how the docs connect (Obsidian does not index dot-folders, so links into `.claude/` show as unresolved there)

## Requirements

- An AI agent capable of reading files and exploring a codebase
- Either network access for that agent (so it can fetch the instructions) or `git` (for the shallow-clone fallback)
- The target repo must have identifiable structure (any language, any framework)
- Obsidian (optional, for graph view)

---

## License

MIT License

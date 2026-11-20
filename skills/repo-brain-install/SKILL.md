---
name: repo-brain-install
description: Use when the user wants to install, set up, upgrade, or refresh repo-brain (the AGENTS.md hub + linked docs/ knowledge base) in a repository, when they mention "repo-brain", "install-obsidian", "give this repo a brain", "AGENTS.md hub", "set up docs for my agent", or ask for a documentation knowledge base that every AI agent can read. Also use when they say the repo has no AGENTS.md, or that an old install-obsidian v1 layout needs upgrading.
---

# repo-brain install

## Overview

`repo-brain` gives a repository an `AGENTS.md` hub that every agent reads first, a one-line `CLAUDE.md`
(`@AGENTS.md`), and a linked `docs/` knowledge base built from that repo's real structure. It is Markdown
instructions, not code — there is no package to install and no build step.

This skill does **not** contain the installer. It gets you to the installer and keeps the run honest.

**Core principle:** the installer is the source of truth. Never reconstruct its phases from memory, and never
summarize an instruction file — you need its exact text.

## When to Use

- User wants repo-brain installed in their repo
- User's repo has no `AGENTS.md`, or they want a docs knowledge base their agent reads
- An `install-obsidian` v1 layout needs upgrading (`CLAUDE.md` holds `## Documentation Map`, docs use `[[wiki-links]]`)
- User wants to re-run or refresh an install that went wrong

**Do NOT use for:** writing ordinary project docs by hand, or maintaining docs in a repo that already has the hub
(that is the `updating-docs` skill shipped by the installer).

## Step 1 — Confirm the target

The target is **the repository the user is working in**, never `repo-brain` itself.

1. Run `git rev-parse --show-toplevel` (or `pwd` when it is not a git repo).
2. Say the path out loud before writing anything.
3. If it is ambiguous, ask. Do not install into a directory you guessed.

## Step 2 — Get the installer verbatim

Resolve every installer path against this base:

```text
https://raw.githubusercontent.com/borncode-app/repo-brain/main/<path>
```

- Entry point: `AGENT-INSTALL.md`
- Fresh install flow: `INSTALL.md`
- v1 upgrade flow: `UPGRADE.md`
- Steps: `PHASES/01-analyze.md` … `PHASES/05-cleanup.md`
- Structures: `TEMPLATES/`

**Fetch it as text, not as a summary.** Some agents pass a fetched page through a summarizer and hand you the
summary; instruction files do not survive that. If your fetch tool summarizes, use the shell instead:
`curl -fsSL <raw-url> -o <scratch>/<name>.md`, then read the file. If the sandbox has no network, ask the user for
a shallow clone (`git clone --depth 1 https://github.com/borncode-app/repo-brain.git <scratch>/repo-brain`) before
doing anything else.

Fetch lazily: `AGENT-INSTALL.md` first, then each file when a step needs it. `AGENT-INSTALL.md` holds the
per-harness fetch table; read it before improvising.

## Step 3 — Route

`AGENT-INSTALL.md` → then `INSTALL.md` → "Before You Start":

- **v1 layout** (`CLAUDE.md` has `## Documentation Map` and `docs/_index.md` exists) → `UPGRADE.md`
- **anything else** → `INSTALL.md`

## Step 4 — Ask for the mode before Phase 2

One sentence, then wait:

> Strict (default: the full standard category set) or adaptive (only the categories your codebase justifies)?

## Step 5 — Stop at every gate

Phase 1 analysis, Phase 2 doc tree, Phase 3 result, and every Phase 5 deletion wait for the user. Never delete a
file the user did not approve individually.

## Step 6 — Finish

- Run `INSTALL.md` → "Post-Install Validation" and report each failure with its reason.
- Report: files created, files modified, mode used, instruction-file migration coverage if the repo had any, and
  the validation result.

## Red Flags

| Thought | Reality |
|---------|---------|
| "I know how repo-brain works, I'll just build the structure" | The phases encode approval gates and migration safety. Reconstructing them loses both. |
| "This fetch returned the gist, that's enough" | A summarized phase file drops constraints. Get the text. |
| "The repo is empty, I'll skip analysis" | A single-file repo still gets a minimal tree from `INSTALL.md` → Troubleshooting. |
| "I'll delete the old rules files now" | Phase 5 requires approval per file. |
| "The user said just do it, so no gates" | "Just do it" authorizes the work, not the deletions or the mode choice. |

## Note for contributors

This is the **only** skill in this repo allowed to name `repo-brain` and its URLs. The skills and rules under
`.claude/` are copied verbatim into arbitrary target repos and must stay generic; this one is the installer's own
front door and is never copied into a target repo.

Because of that split, `npx skills add borncode-app/repo-brain` lists two skills: this one and the generic
`updating-docs`. That is expected — `updating-docs` is meant to arrive with an install, not before one, so install
this skill with `--skill repo-brain-install`.

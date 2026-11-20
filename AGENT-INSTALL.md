# AGENT-INSTALL — Install repo-brain from a URL

> **You are an AI agent.** A human pasted a prompt that points you here so you can install `repo-brain` into the
> repository they are working in, without cloning anything.
> Read this file once, then follow it. Fetch installer files only when a step needs them.

---

## 1. What you are installing

`repo-brain` is Markdown instructions, not code. Installing it gives the target repo:

- an `AGENTS.md` hub that every agent reads first, with the stable rules inline
- a one-line `CLAUDE.md` (`@AGENTS.md`) so Claude Code loads the same hub
- a linked `docs/` knowledge base built from that repo's real structure
- `decisions.md`, `.claude/rules/coding-behavior-rules.md`, and `.claude/skills/updating-docs/SKILL.md`

There is no package to install and no build step.

## 2. Confirm the target repo

- The target is **the repo the human is working in**, never `repo-brain` itself.
- Run `git rev-parse --show-toplevel` (or `pwd`). State the path before you write anything.
- If the path is ambiguous, ask. Do not install into a directory you only guessed.

## 3. Reach the installer files

Use the first method your tools allow.

| Order | Method | How |
|-------|--------|-----|
| 1 | **Fetch** (preferred) | Read `https://raw.githubusercontent.com/borncode-app/repo-brain/main/INSTALL.md` and follow it |
| 2 | **Download** | `curl -fsSL <url> -o <path>`, or `Invoke-WebRequest -Uri <url> -OutFile <path>` on Windows, into a scratch directory outside the target repo |
| 3 | **Shallow clone** | `git clone --depth 1 https://github.com/borncode-app/repo-brain.git <scratch>/repo-brain`, then delete it after Phase 5 |

Do not pick the clone when fetching works. Never edit files under `repo-brain`; read only.

### Fetching rules that change the outcome

Some agents summarize a fetched page instead of giving you its text, and some have no network at all. Instruction
files are worthless summarized, so use the reliable path for your tool.

| Agent | What to do |
|-------|------------|
| **Read tool with a URL, or a fetch that returns the page text** | Fetch directly. Nothing else needed. |
| **Claude Code** | `WebFetch` runs the page through a summarizer and returns the summary, not the file. Use `Bash` instead: `curl -fsSL <raw-url> -o <scratch>/<name>.md`, then `Read` that file. `WebFetch` is fine only for deciding whether the repo exists. |
| **Codex CLI** | Network is off by default in the `workspace-write` sandbox, so `curl` fails. Either run `codex --sandbox danger-full-access`, or ask the human to say yes to one `curl`, or fall back to the shallow clone in the table above. |
| **Cursor, Copilot, and most IDE agents** | Their fetch tool usually returns the page text. Fetch directly, and if what comes back reads like a summary rather than the file, switch to `curl` or the shallow clone. |

A fetch that fails is information, not a dead end: name what you tried, then take the next method in the table.

> **Reached here through `npx skills add`?** The `repo-brain-install` skill in `skills/repo-brain-install/` is the
> same procedure, installed on your machine. Either path works; this file is authoritative when they disagree.

## 4. Resolve relative links against the raw base

`INSTALL.md`, the phase files, and the templates link each other with relative paths such as
`PHASES/01-analyze.md` and `../TEMPLATES/feature-doc.md`. When you fetch instead of clone, resolve every one of
them against:

```text
https://raw.githubusercontent.com/borncode-app/repo-brain/main/<path>
```

Two consequences:

- **Fetch lazily.** Read `INSTALL.md` first, then each phase file when you reach it. Do not load the whole installer into context at once.
- **Copy shipped files from the URL.** `.claude/rules/coding-behavior-rules.md` and `.claude/skills/updating-docs/SKILL.md` are copied verbatim; read each one at the raw URL and write it into the target.

## 5. Run the install

[INSTALL.md](INSTALL.md) is the only source of truth for the steps; this file only tells you how to reach it, plus
the three things a remote install is most likely to drop:

1. **Route first.** INSTALL.md → "Before You Start" decides between a fresh install and [UPGRADE.md](UPGRADE.md) for repos installed with `install-obsidian` (v1 layout: `CLAUDE.md` holds `## Documentation Map` and `docs/_index.md` exists).
2. **Ask for the mode before Phase 2.** `strict` (default: full standard categories) or `adaptive` (only the categories the analysis justifies). Ask in one sentence and wait for the answer.
3. **Stop at the gates.** Phase 1 analysis, Phase 2 doc tree, Phase 3 result, and every Phase 5 deletion wait for the human. Never delete a file the human did not approve one by one.

## 6. Finish

- Run INSTALL.md → "Post-Install Validation" and report every item that fails, with its reason.
- Report back: files created, files modified, mode used, instruction-file migration coverage if the repo had any, and the validation result.
- If fetches and downloads are both blocked, say so and ask the human whether a shallow clone is acceptable. Do not invent the installer from memory.

---

## Related

- [INSTALL.md](INSTALL.md) — the install flow this file starts
- [UPGRADE.md](UPGRADE.md) — for repos installed with `install-obsidian` (v1)
- [README.md](README.md) — project overview
- [PRINCIPLES.md](PRINCIPLES.md) — the design rules the install applies

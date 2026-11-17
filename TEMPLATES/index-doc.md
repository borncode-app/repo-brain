# Template: Index Doc (_index.md)

> Use for: docs/_index.md — the documentation navigation hub
> Location: `docs/_index.md`

---

## Structure

```markdown
# [Project Name] — Documentation Index

> Navigation hub for all project documentation.
> Start here to find what you need.

---

## Quick Links

- [AGENTS.md](../AGENTS.md) — Project hub (every agent reads this first)
- [README.md](../README.md) — User-facing introduction

---

## Project

| Doc | Description |
|-----|-------------|
| [docs/project/<name>.md](project/<name>.md) | [one-line description] |

## Architecture

| Doc | Description |
|-----|-------------|
| [docs/architecture/<name>.md](architecture/<name>.md) | [one-line description] |

## Features

| Doc | Description |
|-----|-------------|
| [docs/features/<name>.md](features/<name>.md) | [one-line description] |

## Integrations

| Doc | Description |
|-----|-------------|
| [docs/integrations/<name>.md](integrations/<name>.md) | [one-line description] |

## Build & Testing

| Doc | Description |
|-----|-------------|
| [docs/build/<name>.md](build/<name>.md) | [one-line description] |
| [docs/testing/<name>.md](testing/<name>.md) | [one-line description] |

## Reference

| Doc | Description |
|-----|-------------|
| [docs/reference/<name>.md](reference/<name>.md) | [one-line description] |

---

## External Resources

- [Link to external docs, APIs, etc. if applicable]

## Optional: Decision Notes
(Only if index structure is intentionally non-obvious.)

- Decision: [what navigation choice was made]
- Why: [reason/tradeoff]
- Impact: [how readers should use this index]
```

## Guidelines

- **Include only categories that have docs** — remove empty sections entirely
- **Every entry must link to a real file** — no placeholders
- **Links are relative to `docs/`** — link text is the path from the repo root, href is the path from this file (`[docs/project/overview.md](project/overview.md)`)
- **Organize by category** matching the folder structure under `docs/`
- **Description should answer** "what will I learn by reading this?"
- Keep this file compact — it's a map, not an encyclopedia
- Prefer signal over volume: do not add low-value entries just to fill categories

---

## Related

- [INSTALL.md](../INSTALL.md) — How this template is used during implementation
- [TEMPLATES/hub-agents-md.md](hub-agents-md.md) — AGENTS.md is the first hub, _index.md is the second
- [PHASES/03-implement.md](../PHASES/03-implement.md) — Phase that creates docs/_index.md

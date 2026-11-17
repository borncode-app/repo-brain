# Template: Integration Doc

> Use for: external tools, libraries, or services with non-trivial usage
> Location: `docs/integrations/<tool-name>.md`

---

## Structure

```markdown
# [Tool/Library Name]

> One-line description of how this tool is used in the project.

---

## Overview
[What is this tool? Why was it chosen? What role does it play in the project?]

## Context Snapshot
[Environment assumptions, trust boundaries, and integration scope.]

## When to Read This

### Trigger

- (fill from doc content)

### Read With

- [docs/path/file.md](../path/file.md) — reason

## Setup
[How to install, configure, or authenticate this tool.
Include version requirements if relevant.]

## Usage in This Project
[How the project actually uses this tool — not generic docs.
Table of files/modules that interact with it and what they do.]

## Configuration
[Project-specific config for this tool.
Table of config keys, values, and purposes.]

## Gotchas
[Common pitfalls when working with this integration in this project.
Things that surprised the team.]

## Decision Trace
(Optional — include only integration choices that affect maintenance.)

- Decision: [what was chosen]
- Why: [reason/tradeoff]
- Impact: [what changes for setup/operations]

---

Related: [docs/path/doc-1.md](../path/doc-1.md) | [docs/path/doc-2.md](../path/doc-2.md)
```

## Guidelines

- **Usage in This Project** is the core value — don't copy the tool's official docs
- Focus on project-specific decisions, not general tool documentation
- Include version constraints if the project is sensitive to versions
- **Gotchas** should capture real problems encountered, not theoretical ones
- Keep setup details practical; link out instead of duplicating vendor docs

---

## Related

- [INSTALL.md](../INSTALL.md) — How this template is used during implementation
- [TEMPLATES/architecture-doc.md](architecture-doc.md) — Architecture may reference integrations
- [TEMPLATES/build-doc.md](build-doc.md) — Build process may depend on integrated tools
- [TEMPLATES/index-doc.md](index-doc.md) — Index doc links to all integration docs

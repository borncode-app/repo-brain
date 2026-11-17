# Template: Architecture Doc

> Use for: structural patterns, subsystem design, layer descriptions
> Location: `docs/architecture/<topic>.md`

---

## Structure

```markdown
# [Architecture Topic]

> One-line description of this architectural aspect.

---

## Overview
[What is this architectural pattern/layer/subsystem?]

## Context Snapshot
[Current boundaries, constraints, and non-goals for this architecture area.]

## When to Read This

### Trigger

- (fill from doc content)

### Read With

- [docs/path/file.md](../path/file.md) — reason

## Structure
[Visual representation — tree diagram, layer diagram, or composition table.
Show how parts relate to each other.]

## Component Reference
[Table of components with their location and responsibility.
Only include non-obvious components.]

## How to Extend
[When someone needs to add to this architecture, what do they do?
Step-by-step guide for common extension patterns.]

## Decision Trace
(Optional — keep to major tradeoffs only.)

- Decision: [what was chosen]
- Why: [reason/tradeoff]
- Impact: [what contributors must preserve]

## Design Origin
(Omit if not applicable)

---

Related: [docs/path/doc-1.md](../path/doc-1.md) | [docs/path/doc-2.md](../path/doc-2.md)
```

## Guidelines

- **Structure** section should make the architecture visible at a glance
- **How to Extend** is critical — it's the main reason this doc exists
- Architecture docs should link to feature docs that implement the patterns
- Do NOT list every file — only the ones that define the architecture
- Keep Decision Trace concise; include only durable, high-impact choices

---

## Related

- [INSTALL.md](../INSTALL.md) — How this template is used during implementation
- [TEMPLATES/feature-doc.md](feature-doc.md) — Feature docs link to architecture docs
- [TEMPLATES/reference-doc.md](reference-doc.md) — Reference docs complement architecture docs
- [TEMPLATES/index-doc.md](index-doc.md) — Index doc links to all architecture docs

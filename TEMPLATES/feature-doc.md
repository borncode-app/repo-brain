# Template: Feature Doc

> Use for: user-facing features with non-obvious workflows
> Location: `docs/features/<feature-name>.md`

---

## Structure

```markdown
# [Feature Name]

> One-line description of what this feature does.

---

## Overview
[What is this feature? Why does it exist? What problem does it solve?]

## Context Snapshot
[Scope, boundaries, and assumptions for this feature in its current state.]

## When to Read This

### Trigger

- (fill from doc content)

### Read With

- [docs/path/file.md](../path/file.md) — reason

## Flow / User Journey
[Step-by-step walkthrough of how a user interacts with this feature.
Use numbered steps or a sequence diagram if helpful.]

## Key Files
[Table of files involved in this feature and their roles.
Only include files that are NOT obvious from the feature name.]

## Configuration
[Any config options related to this feature.
Table format: config key, default, purpose.]

## Decision Trace
(Optional — only for meaningful product/engineering tradeoffs.)

- Decision: [what was chosen]
- Why: [reason/tradeoff]
- Impact: [what implementers/operators must know]

## Design Origin
- Spec: [path/to/spec.md](../../path/to/spec.md)
- Plan: [path/to/plan.md](../../path/to/plan.md)
(Include only if a spec/plan exists. Omit entire section if not.)

---

Related: [docs/path/doc-1.md](../path/doc-1.md) | [docs/path/doc-2.md](../path/doc-2.md)
```

## Guidelines

- **Flow section** is the most important — it's what makes this doc valuable
- **Key Files** should explain WHY each file matters, not just list them
- **Configuration** is optional — omit if feature has no config
- Every feature doc should link to at least one architecture doc
- Keep docs small and focused; split only when retrieval quality improves

---

## Related

- [INSTALL.md](../INSTALL.md) — How this template is used during implementation
- [TEMPLATES/architecture-doc.md](architecture-doc.md) — Feature docs link to architecture docs
- [TEMPLATES/project-doc.md](project-doc.md) — Project overview connects to feature docs
- [PHASES/03-implement.md](../PHASES/03-implement.md) — Phase that creates feature docs

# PRINCIPLES — Design Philosophy

> The rules that guide every documentation decision.
> Read this before designing any doc tree.

---

## Core Principles

### 1. Hybrid by design: installer core + inspired knowledge practices

Keep the repo-brain installer core intact (phase flow, stable rules, migration safety, practical gates),
and apply llm-wiki-inspired practices as a complementary layer:

- Modular docs (small, focused topics)
- Cross-linking for usable graph navigation
- Living knowledge that updates with real changes
- Context/rationale-first explanations

The inspired layer must not replace or weaken installer requirements.

### 2. Docs follow the codebase, not the other way around

Documentation structure must reflect the ACTUAL repo structure. Do not impose a predefined folder tree. Instead:

- Analyze what the repo actually contains
- Identify real subsystems, workflows, and important files
- Create docs only where they add genuine value

### 3. Hub-and-spoke architecture

```
AGENTS.md (hub)  <──  CLAUDE.md (one line: @AGENTS.md)
    ├── links to → docs/_index.md (navigation)
    ├── links to → docs/project/* (project knowledge)
    ├── links to → docs/architecture/* (structure knowledge)
    ├── links to → docs/features/* (behavior knowledge)
    └── links to → docs/reference/* (stable reference)
```

- **AGENTS.md** = front door for every agent. Compact. Link-heavy. No encyclopedia.
- **CLAUDE.md** = a pointer to that door, not a second one: a single import line, so Claude Code enters through the same hub.
- **docs/_index.md** = second door. Full navigation map.
- **Category folders** = rooms. Each doc = one focused topic.

### 4. Every doc earns its existence

Before creating a doc, answer:

- Does this doc contain information NOT derivable from reading the code?
- Does this doc help a newcomer (human or AI) understand the system faster?
- Would this doc be missed if it were deleted?

If the answer to all three is "no", do not create it.

### 5. Link generously, duplicate never

- Use standard relative Markdown links: `[docs/project/overview.md](../project/overview.md)`
  - **href** — the path relative to the file that contains the link, with the `.md` extension
  - **text** — in navigation sections (Read First, Task Routing, Documentation Map, Read With, Related), the target's path from the repo root
- When information exists elsewhere, link to it instead of rewriting it
- Every doc should have a `Related:` section at the bottom

One format serves every reader: an agent opens the path in the link text, GitHub and editors follow the href, and Obsidian draws the same link in its graph view.

### 6. AGENTS.md is for AI onboarding

`AGENTS.md` is the instruction file agents share: Codex, Cursor, GitHub Copilot, and [many others](https://agents.md) read it directly, and Claude Code reads it through the `@AGENTS.md` import in `CLAUDE.md`. Whatever every agent must know goes here, once.

AGENTS.md should contain ONLY:

- Project identity (name, stack, version)
- Stable rules (non-negotiable, one line each)
- Read-first links
- Quick commands
- Working rules
- Documentation map (links to all docs)
- Key warnings for risky areas
- Doc Workflow (so AI knows to auto-create docs for new features)

AGENTS.md should NOT contain:

- Detailed architecture explanations
- Full dependency lists
- Code examples
- Troubleshooting guides

### 7. Design Origin tracks provenance

When a feature doc was created from a design spec or implementation plan, add a `## Design Origin` section:

```markdown
## Design Origin
- Spec: [path/to/spec.md](../../path/to/spec.md)
- Plan: [path/to/plan.md](../../path/to/plan.md)
```

This helps AI agents understand where a feature came from and find the original design decisions.

### 8. Optimize for the graph, but usefulness first

- Links make the doc graph meaningful — on GitHub, in an editor, or in Obsidian graph view
- Hub docs (AGENTS.md, _index.md) should connect to many spokes
- Spoke docs should connect to related spokes
- But never add links that don't help navigation — visual prettiness is secondary

### 9. Every doc must answer "when should I read this?"

Before an AI agent can use a doc, it needs to know when to load it into context.
Every doc (except hub and index docs) must include:

- **Trigger** — task-based situations that require this doc
- **Read With** — sibling docs needed alongside this one

Link format in Read With:
`[docs/path/file.md](../path/file.md) — reason`

One link serves both purposes:
- link text → the real path from the repo root, so an AI agent navigates straight to the file
- href → GitHub, editors, and Obsidian resolve it and draw the graph edge

### 10. Context and rationale beat file-summary dumps

Each substantive doc should capture context that code alone does not explain:

- Why this approach exists
- What tradeoffs were accepted
- What to preserve when changing it

If a section only repeats obvious file content, replace it with links or remove it.

---

## Category Guide

| Category | When to create | Key questions to answer | Template |
|----------|---------------|------------------------|----------|
| `docs/project/` | Always | What is this? What changed? What's broken? | [TEMPLATES/project-doc.md](TEMPLATES/project-doc.md) |
| `docs/architecture/` | When codebase has identifiable structure | How does it fit together? What are the layers? | [TEMPLATES/architecture-doc.md](TEMPLATES/architecture-doc.md) |
| `docs/features/` | When features have non-obvious workflows | How does this feature work end-to-end? | [TEMPLATES/feature-doc.md](TEMPLATES/feature-doc.md) |
| `docs/integrations/` | When external tools/libraries have non-trivial usage | How is [tool] used? Where are the binaries? | [TEMPLATES/integration-doc.md](TEMPLATES/integration-doc.md) |
| `docs/build/` | When build/packaging is non-trivial | How to build? How to release? | [TEMPLATES/build-doc.md](TEMPLATES/build-doc.md) |
| `docs/testing/` | When testing approach matters | How to test? What's the strategy? | [TEMPLATES/testing-doc.md](TEMPLATES/testing-doc.md) |
| `docs/reference/` | When config/paths/constants need explanation | What does this constant mean? How does path resolution work? | [TEMPLATES/reference-doc.md](TEMPLATES/reference-doc.md) |

Not every repo needs every category. Create only what the codebase justifies.

---

## Anti-Patterns to Avoid

| Anti-pattern | Why it's bad |
|-------------|-------------|
| One doc per folder regardless of value | Creates noise, dilutes graph |
| Copying README into docs/overview.md | Duplication, maintenance burden |
| Giant AGENTS.md with everything | AI context waste, hard to update |
| Rules or hub content kept in an agent-specific file | Other agents never load it, and the copies drift apart |
| Empty docs "for completeness" | Worse than no docs — misleading |
| Static hardcoded paths in templates | Breaks when used in different repos |
| No links between docs | Isolated nodes, graph is useless |
| `[[wiki-links]]` | Plain text on GitHub; an agent has to guess the path and extension |
| "Related" section with bare links only | AI can't tell when or why to follow the link |
| Too many low-value docs created "just in case" | Knowledge drift, maintenance burden, weak signal |
| File-by-file summaries without rationale | Not useful for decision-making or onboarding |

---

## Success Criteria

The documentation system is successful when:

1. Any AI agent can read AGENTS.md and immediately know where to find information
2. The link graph shows meaningful clusters, not isolated islands
3. Adding a new feature doc is a 5-minute task (template + fill + link)
4. No doc contains information that's obvious from reading the code
5. Every doc has at least 2 incoming links from other docs

---

## Related

- [INSTALL.md](INSTALL.md) — How these principles are applied in practice
- [README.md](README.md) — Project overview
- [PHASES/01-analyze.md](PHASES/01-analyze.md) — Phase 1 uses these principles to analyze repos
- [PHASES/02-design.md](PHASES/02-design.md) — Phase 2 designs doc trees following these rules
- [PHASES/03-implement.md](PHASES/03-implement.md) — Phase 3 implements docs based on these principles

### Template References

| Principle | Relevant Template |
|-----------|------------------|
| Hub-and-spoke architecture | [TEMPLATES/hub-agents-md.md](TEMPLATES/hub-agents-md.md), [TEMPLATES/index-doc.md](TEMPLATES/index-doc.md) |
| Every doc earns its existence | [TEMPLATES/project-doc.md](TEMPLATES/project-doc.md), [TEMPLATES/feature-doc.md](TEMPLATES/feature-doc.md) |
| Link generously, duplicate never | [TEMPLATES/architecture-doc.md](TEMPLATES/architecture-doc.md), [TEMPLATES/reference-doc.md](TEMPLATES/reference-doc.md) |
| Optimize for the graph | [TEMPLATES/integration-doc.md](TEMPLATES/integration-doc.md), [TEMPLATES/testing-doc.md](TEMPLATES/testing-doc.md) |

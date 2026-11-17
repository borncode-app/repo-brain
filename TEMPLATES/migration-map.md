# Template: Migration Map

> Use for: section-by-section migration planning and verification (legacy instruction files such as `CLAUDE.md` and `.claude/rules/*`, and old docs)
> Location: `docs/project/migration-map.md` (or equivalent design artifact in Phase 2 output)

---

## Structure

```markdown
# Migration Map

> Source-to-destination map for migrated documentation.

---

## When to Read This

### Trigger

- (fill from doc content)

### Read With

- [docs/path/file.md](../path/file.md) — reason

## Scope
- Source files: [e.g., CLAUDE.md, .claude/rules/stable-rules.md, old-doc.md]
- Migration mode: [strict/adaptive]
- Owner: [human/agent]
- Hybrid intent: [how installer core is preserved while inspired-layer improvements are applied]

## Section Mapping
| Source file | Source section | Destination file | Destination section | Migration method (rewrite/link/keep) | Verification evidence | Status |
|-------------|----------------|------------------|---------------------|---------------------------------------|-----------------------|--------|
| CLAUDE.md | [section name] | AGENTS.md | [heading] | rewrite | [dest heading + summary] | mapped |
| old-doc.md | [section name] | [docs/path/file.md](../path/file.md) | [heading] | rewrite | [dest heading + summary] | mapped |

Status values:
- `mapped` — planned destination exists
- `verified` — destination implemented and checked
- `uncertain` — partial or ambiguous migration
- `blocked` — cannot migrate without human decision

## Coverage Summary
- Total meaningful source sections: [N]
- Mapped sections: [N]
- Verified sections: [N]
- Uncertain/blocked sections: [list or "none"]

## Drift Guard Notes
- [confirm no duplicate-topic docs were introduced during migration]
- [confirm key rationale context was preserved, not only file references]

## Removal Candidates
| File | Eligible for removal? | Reason | Preconditions |
|------|------------------------|--------|---------------|
| .claude/rules/stable-rules.md | no/yes | [why] | all sections verified + human approval |

> `AGENTS.md` is the hub and is never removed. `CLAUDE.md` is never removed either: once its sections are verified, its content is replaced by the one-line import `@AGENTS.md`.

---

Related: [docs/path/doc-1.md](../path/doc-1.md) | [docs/path/doc-2.md](../path/doc-2.md)
```

## Guidelines

- Treat migration as section-level work, not file-level only
- Do not mark a file removable until all meaningful sections are verified
- Keep uncertain mappings visible and unresolved until human confirms
- Reuse this map in Phase 2 planning, Phase 3 verification, and Phase 5 cleanup
- Validate that migrated docs stay practical and high-signal (no template-only content)

---

## Related

- [INSTALL.md](../INSTALL.md) — Main instruction flow with strict/adaptive mode and definition of done
- [PHASES/02-design.md](../PHASES/02-design.md) — Migration mapping is required here
- [PHASES/03-implement.md](../PHASES/03-implement.md) — Migration coverage gate uses this map
- [PHASES/05-cleanup.md](../PHASES/05-cleanup.md) — Cleanup verification references this map

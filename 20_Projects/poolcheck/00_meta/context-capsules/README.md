# Context Capsules

Context capsules are dense, retrieval-optimized notes that compress recurring operational questions from a project's `00_meta/` files.

## When to create a capsule

A capsule is justified only if ALL three gates pass:

1. **3+ FACT-labeled evidence entries** exist in the project's populated `00_meta/` notes for the domain
2. **Meaningful operational boundary** — the domain represents a recurring question agents/humans would ask
3. **Token reduction** — the capsule would save context vs. reading the full meta notes

## Rules

- Filename format: `capsule-<domain>.md` (lowercase, hyphenated)
- Target length: ≤60 lines of content (excluding frontmatter). Hard max: 80 lines.
- Use the standard vault property schema with `type: context-capsule`
- Only FACT-labeled items count toward the 3-evidence minimum
- INFERENCE items must go in a separate "Inference notes" subsection
- A capsule must NOT duplicate `_project.md`, `repo-map.md`, or `architecture-index.md`
- All AI-created capsules must have `reviewed: false`
- If a capsule topic overlaps across projects, note the overlap — do NOT create a global capsule

## Staleness

Per STALENESS_POLICY, review capsules on the same schedule as their parent note type (typically 90 days). Use 45-day review for volatile domains (build-test, deployment, auth, ai-integrations).

## Location

```
project-name/
└── 00_meta/
    └── context-capsules/
        ├── capsule-build-test.md
        ├── capsule-database.md
        └── capsule-sync.md
```

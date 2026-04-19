---
type: system
scope: global
status: active
reviewed: true
tags: [system, protocol]
---

# Retrieval Protocol

Defines what to read, in what order, and when to stop — for any AI tool operating in this vault.

## Core Rule: Single-Project Isolation

**Never load notes from both `unionforge-ai` and `arkaan` in the same retrieval pass** unless the user explicitly requests a cross-project comparison, migration plan, or shared-pattern analysis. Load only the project relevant to the current task.

## Tier Budget

Start at **Tiers 0–2 only**. Escalate to Tier 3+ only if the needed fact is still unresolved after reading capsules. Most coding tasks should never need Tier 4 or 5.

## Retrieval Tiers

| Tier | What to Read | When to Stop |
|------|-------------|--------------|
| 0 | `00_System/AI/VAULT_RULES.md` | Always read — non-negotiable |
| 1 | `_project.md` + `current-focus.md` for the active project | Stop here if the task context is already clear |
| 2 | Context capsule(s) matching the task domain | **Stop here for most tasks** |
| 3 | Full `00_meta/` notes: `repo-map`, `architecture-index`, `authority-map`, `dependency-map` | Only if Tier 2 left the question unresolved |
| 4 | Project `wiki/` pages | Only for architecture, cross-cutting patterns, or design history |
| 5 | `raw/` source files | Last resort — only when vault content conflicts with observed repo state |

## Task-Type Load Tables

### Normal Coding Task

1. Tier 0 — VAULT_RULES
2. Tier 1 — `_project.md`, `current-focus.md`
3. Tier 2 — `capsule-build-test.md` (if running tests or builds)
4. Tier 2 — `capsule-database.md` (if touching schema or queries)
5. Stop. Execute task.

### Debugging

1. Tier 0 — VAULT_RULES
2. Tier 1 — `current-focus.md` (confirms recent changes and verified state)
3. Tier 2 — capsule matching the failing domain
4. Tier 3 — `architecture-index.md` § Failure Surfaces (if root cause is unclear)
5. Tier 3 — `repo-map.md` § Key Scripts (if the failing command is ambiguous)
6. Stop. Do not speculatively read further.

### Architecture / Refactor Work

1. Tier 0 — VAULT_RULES
2. Tier 1 — `_project.md`, `current-focus.md`
3. Tier 2 — all capsules for the project (scan all, read relevant ones)
4. Tier 3 — `architecture-index.md`, `authority-map.md`, `dependency-map.md`
5. Tier 4 — project `wiki/` pages if design history is needed
6. Consult `authority-map.md` before any change that touches generated files, auth, or external APIs.

## When to Consult `authority-map.md`

Read `authority-map.md` before:
- Any change to files listed there as generated or owned by external tools
- Any modification to auth, RLS, or secrets handling
- Any change that could introduce circular package dependencies

## When Capsules Are Preferred Over Meta Notes

Use a context capsule instead of the full meta note when:
- The question is operational (e.g., "what command do I run?", "what's the schema for X?")
- You need 1–3 specific facts, not a full structural overview
- Time or token budget is constrained

Use the full meta note when:
- The capsule's `source-of-truth notes` section indicates the full note has deeper context
- The capsule has `reviewed: false` and the decision is high-stakes
- The capsule's staleness threshold (per STALENESS_POLICY) has been exceeded

## Contradiction Resolution

**Repo truth always overrides vault summaries.** If observed repo state (file contents, test output, build output) conflicts with a vault note:

1. Do not silently ignore the conflict.
2. Note the discrepancy: "Vault says X, repo shows Y."
3. Trust the repo for the immediate task.
4. Flag the stale vault note: add `> **Stale** — last verified YYYY-MM-DD. Needs review.` to the note body.
5. Update the vault note if you have confirmed evidence. Do not update from inference.

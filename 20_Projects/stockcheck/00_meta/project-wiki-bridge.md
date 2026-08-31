---
type: reference
scope: project
project: stockcheck
status: active
reviewed: true
tags: [bridge, reference]
---

# Project Wiki Bridge — StockCheck

## Role of Project Wiki

The StockCheck `.project-wiki/` (at canonical repo root) is the **durable memory layer** — it stores decisions, requirements, architecture documentation, ADRs, project state, and indexed knowledge.

## Role of Obsidian Agent Memory

This vault is a **compact operational continuation layer** — it stores only the minimum facts needed to resume work efficiently between sessions. It does NOT duplicate Project Wiki content.

## Capsule → Project Wiki Escalation

When a context capsule's answer is insufficient:

1. Check `20_Projects/stockcheck/_project.md` for the canonical repo path.
2. Read `.project-wiki/INDEX.md` for the project knowledge index.
3. Navigate to the specific linked canonical page from INDEX.
4. If still unresolved, use Graphify (architecture) or Serena (symbols/references) against the repo.

**Do not load the full Project Wiki in a single pass.**

## Repo/Tests Override

If any memory layer (Project Wiki or Obsidian) conflicts with current repo code, Git history, migrations, or passing tests → **trust the repo/tests.** Flag the conflict but do not silently ignore it.

## Tool Roles

| Tool | When to Use |
|------|-------------|
| Graphify | Current architecture, dependency maps, codebase queries |
| Serena | Symbol lookups, references, declarations |
| Project Wiki | Durable requirements, decisions, project state |
| Obsidian Memory | Session continuation context |

## BSV2 Prohibition

**BSV2 and real business data are completely off-limits.** Agents must never connect to, query, inspect, audit, migrate, seed, backfill, insert, update, or delete BSV2. DEV/local/test databases ARE allowed when the canonical StockCheck repository rules permit them. Database work must follow the canonical repository AGENTS.md and environment guards. Never treat DEV/test data as evidence of BSV2 state. Do not inspect StockCheck env files.

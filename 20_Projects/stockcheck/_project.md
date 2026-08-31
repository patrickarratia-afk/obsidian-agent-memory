---
type: project
scope: project
project: stockcheck
area: software-engineering
status: active
source_date: 2026-08-30
reviewed: true
owner: patrick
aliases: [StockCheck, stockcheck-app]
tags: [project, stockcheck]
---

# Project: StockCheck

## Canonical Repo

`/home/patrick/Apps/Bodega V2/Bodega`

## Purpose

Lightweight operational-memory layer for StockCheck development sessions. This vault stores only the minimum continuation context needed to resume work efficiently.

**It does not duplicate the Project Wiki.**

## Authority Hierarchy

| Priority | Source | Role |
|----------|--------|------|
| 1 | Current repo code, Git history, migrations, passing tests | Ultimate source of truth |
| 2 | `.project-wiki/` at canonical repo path | Durable decisions, requirements, architecture, project state |
| 3 | This Obsidian vault | Compact operational context and session continuity |

**Resolution rules:**
- Obsidian vs Project Wiki → prefer Project Wiki unless repo code disproves it
- Either memory layer vs repo/tests → trust repo/tests

## Path to Durable Knowledge

Start here: `20_Projects/stockcheck/00_meta/` → escalate to `.project-wiki/INDEX.md` → escalate to repo/tests/Graphify/Serena.

## Context Capsules

`20_Projects/stockcheck/00_meta/context-capsules/`
Capsules are FACT-only, ≤ 60 lines (hard max 80). They reference canonical Project Wiki pages for deeper context. Do not copy Project Wiki content into capsules.

## BSV2 Protection

**BSV2 and real business data are completely off-limits.** Agents must never connect to, query, inspect, audit, migrate, seed, backfill, insert, update, or delete BSV2. DEV/local/test databases ARE allowed when the canonical StockCheck repository rules permit them. Database work must follow the canonical repository AGENTS.md and environment guards. Never treat DEV/test data as evidence of BSV2 state. Do not inspect StockCheck env files.

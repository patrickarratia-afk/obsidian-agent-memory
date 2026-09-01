---
type: reference
scope: project
project: poolcheck
status: active
reviewed: true
tags: [focus, active]
---

# Current Focus — PoolCheck

## Canonical Baseline

Branch: `main`

HEAD:

`73246d6 Add provider operational status filtering`

Working tree was clean at the close of P1 7E-A.

## Recently Completed

- [x] Facility foundation — Organization → Facility → Pool
- [x] Facility CRUD API and Pool assignment contract
- [x] Facility-aware Pool filtering
- [x] Provider Facility portfolio enrichment/filter
- [x] Provider operational-status enrichment/filter
- [x] Canonical Project Wiki 1.4.0 installed and validated (0 errors / 0 warnings)

P1 portfolio filtering dimensions now covered:

- client / organization
- Facility
- Pool/search
- operational status

## Current Objective

P1 7E-B — Facility Management UI for owner admins.

Expected scope:

- `/facilities` admin-only management route
- navigation entry `Instalaciones`
- Facility list
- loading/error/empty states
- create Facility
- rename Facility
- delete Facility with confirmation
- friendly handling of `FACILITY_IN_USE`
- responsive behavior consistent with existing PoolCheck UI

## Explicitly Deferred

Do not fold these into 7E-B:

- Pool → Facility assignment UI
- provider Facility management
- Facility hierarchy redesign
- Facility grants/inheritance
- location → Facility conversion/backfill
- DB schema/migrations
- provider status N+1 optimization
- unrelated redesign

## Known Non-Blocking Technical Debt

Provider portfolio operational-status enrichment currently performs one latest-measurement lookup per authorized Pool.

This N+1 behavior passed review and is intentionally deferred unless real portfolio scale makes batching necessary.

## Workflow

For significant changes:

1. inspect
2. discuss
3. decide
4. implement
5. validate
6. review diff/status
7. commit when explicitly authorized
8. push when explicitly authorized
9. update operational memory only for meaningful milestones/decisions
10. close

Do not repeat already-closed audits without new evidence.

## Next Session

Before implementing 7E-B:

1. read `VAULT_RULES`
2. read `_project`
3. read this `current-focus`
4. confirm Git branch/status/HEAD
5. inspect exact auth, route, navigation, CRUD and generated Facility-hook patterns
6. use Serena when useful
7. use Graphify only if architectural dependency information is genuinely needed

Current preferred implementation model while native Codex quota is unavailable:

DeepSeek V4 Flash through Hermes/OpenRouter.

A GPT-5.5 review should be used for sensitive authorization/permission changes when quota is available.

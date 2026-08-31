---
type: reference
scope: project
project: stockcheck
status: active
reviewed: true
tags: [focus, active]
---

# Current Focus — StockCheck

## Active Task

Pilot Path QA + Hardening.

Architecture decision: StockCheck is ready with conditions for a controlled accompanied pilot. Current work is QA/hardening, not a new product feature.

## Recently Completed

- [x] Frontend pure QA tests (`e374a63`) — 53 Node `node:test` frontend pure tests passed; typecheck passed; no new test dependency
- [x] Frontend redesign Phase 1 — design system foundations (`af5de16`)
- [x] Frontend redesign Phase 2 — app shell + inventory workspace (`d90d287`)
- [x] Frontend redesign Phase 3 — Product Detail + Kardex (`f713a46`)
- [x] Frontend redesign Phase 4 — Commercial (`98754d1`)
- [x] Frontend redesign Phase 5 — Production (`fa89ac1`)
- [x] Pilot Onboarding + Simple Mode Readiness (`324afd6`)
- [x] Project Wiki installed and committed in canonical repo
- [x] Obsidian Agent Memory scaffold created for StockCheck

## Verified Baseline

| Check | Status |
|-------|--------|
| Build | See .project-wiki/ for current baseline |
| Tests | See .project-wiki/ for current baseline |

## Next Session

Run existing backend pilot-critical test suite against DEV only (`stockcheck_dev`), then perform manual browser QA across onboarding/readiness X/4, product create/import, purchase, sale, Kardex/traceability, incoming documents, company switching/isolation, Modo simple / Avanzado navigation, and laptop/mobile sanity.

BSV2 and real business data remain prohibited. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

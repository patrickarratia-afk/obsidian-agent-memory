---
type: context-capsule
scope: project
project: stockcheck
domain: pilot-path-qa-hardening
status: active
reviewed: false
source_date: 2026-09-01
owner: patrick
aliases: [pilot-qa, pilot-hardening, pilot-path-qa]
tags: [capsule, pilot, qa, hardening]
---

# Pilot Path QA + Hardening — StockCheck Context Capsule

## Canonical Repo
`/home/patrick/Apps/Bodega V2/Bodega`

## Active Milestone
Pilot Path QA + Hardening is ready for Controlled Pilot Session 1, but is not formally closed while current canonical memory policy still requires mobile QA for formal closure.

## Architecture Decision
Final technical review result: READY WITH CONDITIONS for a controlled laptop/web pilot. Current work is real-user pilot evidence, not speculative UI polish or a new product feature.

## Completed Sub-steps
- Current canonical commit: `993da6f` (`Polish operational workspace consistency`).
- Final readiness evidence captured: frontend pure QA 53/53; backend pilot-critical QA previously passed in DEV; purchase/sale/stock/Kardex manual QA passed; production QA passed; company isolation QA passed; laptop visual/responsive sanity passed; performance issue fixed; cross-screen consistency passes completed; no repo/product changes required before pilot.
- Cross-screen consistency passes landed at `64f592b`, `8170df3`, and `993da6f`; approved visual consistency now covers Inventory, Bandeja / Incoming Documents, Ventas, Commercial / Compras-Ventas, Kardex, Production, and Recipes.
- Preserved contracts across consistency passes: mobile behavior where checked, no business logic changes, no API/SII semantics changes, and recipe behavior preserved.
- Inventory navigation performance hardening landed at `9dc60bb`; validation included 53/53 frontend pure tests, typecheck, static Expo export, and manual production-build QA at `http://localhost:8082` confirming fast navigation.
- Frontend pure QA coverage and backend pilot-critical QA landed at `e374a63`; backend DEV verification covered purchase, sale, stock/Kardex, insufficient-stock rejection, voids, production completion/void, cost handling, and write-off behavior.

## Next Step
Execute Controlled Pilot Session 1: 60–90 minutes guided, laptop/web only, one real primary user plus one supervisor/admin. Session 2 should be 60–90 minutes with reduced prompting. Add a second user only after the core loop works without blockers.

For local frontend browser QA, use `http://localhost:8082`; do not use `127.0.0.1` because backend CORS treats it as a different origin.

Do not perform more speculative UI polish before real-user evidence.

## Pilot Scope
- Laptop/web only; mobile remains out of scope for this controlled pilot and required for formal milestone closure if current canonical memory policy says so.
- One real primary user, one supervisor/admin, DEV/local/pilot data only, backend/PostgreSQL connected, known pilot company/companies, no public SaaS assumptions.
- In scope: Inventory, Purchases, Sales, Commercial / Compras-Ventas, Bandeja / Incoming Documents, Kardex, Production, Recipes, company switching/isolation, simple/advanced navigation.
- Out of scope: mobile, automatic SII connector, public SaaS, public signup, billing, BSV2, major new modules, broad refactors.

## Stop Conditions
Stop if data crosses companies; stock becomes incorrect; sale/production succeeds beyond available stock; a record saves under the wrong company; local fallback appears during a real-write pilot flow; latency/double-click causes a duplicate transaction; an irreversible transaction issue appears; a core purchase/sale/production flow cannot continue; or any workflow attempts to use BSV2.

## Issue Classification
Use BLOCKER, IMPORTANT, POLISH, FUTURE.

## Safety Boundary
BSV2 and real business data are completely off-limits. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

## Known Non-blocking Issue
`splitCsvLine` has a pre-existing CSV edge case where quoted empty fields can parse incorrectly. Do not promote it to a blocker unless later QA proves impact.

## Operational Memory Note
Obsidian materially reduced StockCheck context retrieval in A/B testing and should remain part of the standard StockCheck agent workflow after milestone-closing or operationally significant commits.

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

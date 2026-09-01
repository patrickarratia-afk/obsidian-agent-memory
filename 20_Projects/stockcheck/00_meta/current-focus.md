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

Controlled Pilot Session 1 for Pilot Path QA + Hardening.

Architecture decision: StockCheck is READY WITH CONDITIONS for a controlled laptop/web pilot. Current work is real-user pilot evidence, not speculative UI polish or a new product feature.

## Recently Completed

- [x] Final technical review for controlled laptop/web pilot (`993da6f`) — READY WITH CONDITIONS for a controlled pilot using DEV/local/pilot data, backend/PostgreSQL connected, known pilot company/companies, one real primary user, and one supervisor/admin; no repo/product changes required before pilot; milestone is not formally closed while canonical memory policy still requires mobile QA for formal closure
- [x] Cross-screen consistency pass 3 (`993da6f`) — Commercial / Compras-Ventas, Kardex, Production, and Recipes consistency polish captured: Commercial compact search/clear behavior, standardized header actions, and improved visual consistency; Kardex standardized header actions plus bounded operational table viewport with visible vertical scrollbar and accessible in-viewport horizontal scrollbar aligned with Inventory; Production compact command area, standardized header actions, and bounded table viewport with accessible scrollbars; Recipes full consistency review, standardized header actions, shared bounded table viewport, and preserved recipe behavior; visual QA passed / good enough; no business logic or API behavior changed
- [x] Cross-screen consistency pass 2 (`8170df3`) — Ventas workspace alignment captured: Ventas is now the clear primary title with company context secondary; `+ Proyección` and `+ Venta real` remain directly accessible; duplicate `Acciones rápidas` card removed; month filtering moved into compact toolbar/chips; summary KPI blocks compacted; content starts materially higher; sales cards/table treatment flattened and aligned with Inventory/Bandeja density/header conventions; `+ Proyección` contrast corrected; mobile behavior preserved; visual QA passed; no business logic, API, or sales semantics changed
- [x] Cross-screen consistency pass 1 (`64f592b`) — captured Inventory micro-polish plus Incoming Documents / Bandeja redesign alignment: Inventory header top spacing was slightly increased with density/table layout unchanged; Documents now has a compact page header, primary `+ Documento`, grouped SII actions, compact search/summary, preserved status/target filters, table behavior visually aligned with Inventory, one horizontal scrollbar, visible vertical scrollbar, frozen Proveedor / N° doc. / Fecha columns, preserved header/data alignment, mobile behavior verified, and visual QA passed; no business logic or API/SII semantics changed
- [x] Inventory visual redesign (`2f37b16`) — redesigned inventory workspace to be denser and table-first: `Inventario` is the primary header anchor, search moved closer to title/content, actions and summary were compacted, filters and sort merged into a compact toolbar, the table starts materially higher and consumes more viewport, frozen Product column and horizontal scroll were preserved with one visible bottom horizontal scrollbar, vertical scrollbar remained visible, headings/data stayed aligned, mobile behavior was retained, and visual QA passed
- [x] Inventory navigation performance hardening (`9dc60bb`) — cached `Intl.NumberFormat` formatters, memoized/stabilized `HomeInventoryView` props and callbacks, removed unused unstable props, and memoized committed/expected maps; 53/53 frontend pure tests passed, typecheck passed, static Expo export passed, and manual production-build QA at `http://localhost:8082` confirmed fast navigation again
- [x] Backend pilot-critical QA (`e374a63`) — `backend/npm run test:pilot-critical` passed completely against confirmed DEV database `stockcheck_dev`; working tree stayed clean and HEAD remained `e374a63`
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

Execute Controlled Pilot Session 1: a 60–90 minute guided laptop/web session with one real primary user and one supervisor/admin. Add a second user only after the core loop works without blockers.

Do not perform more speculative UI polish before real-user evidence. Do not mark Pilot Path QA + Hardening formally closed while mobile QA remains required by current canonical memory policy.

For StockCheck frontend local browser testing, use `http://localhost:8082`; do not use `127.0.0.1` because backend CORS treats it as a different origin.

Pilot scope is laptop/web only, DEV/local/pilot data only, backend/PostgreSQL connected, known pilot company/companies, no public SaaS assumptions. In scope: Inventory, Purchases, Sales, Commercial / Compras-Ventas, Bandeja / Incoming Documents, Kardex, Production, Recipes, company switching/isolation, and simple/advanced navigation. Out of scope: mobile, automatic SII connector, public SaaS, public signup, billing, BSV2, major new modules, and broad refactors.

Stop the pilot if data crosses companies, stock becomes incorrect, sale/production succeeds beyond available stock, a record saves under the wrong company, local fallback appears during a real-write pilot flow, latency/double-click causes a duplicate transaction, an irreversible transaction issue appears, a core purchase/sale/production flow cannot continue, or any workflow attempts to use BSV2.

Issue classification during pilot: BLOCKER, IMPORTANT, POLISH, FUTURE.

BSV2 and real business data remain prohibited. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

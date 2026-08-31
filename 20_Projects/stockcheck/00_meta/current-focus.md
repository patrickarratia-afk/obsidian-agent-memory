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

Perform manual browser QA across onboarding/readiness X/4, manual product creation, CSV/XLS/XLSX import, duplicate behavior, purchase, sale, insufficient-stock UX, Kardex/traceability, incoming documents, company switching/isolation, Modo simple / Avanzado navigation, laptop layout, and mobile layout.

For StockCheck frontend local browser testing, use `http://localhost:8082`; do not use `127.0.0.1` because backend CORS treats it as a different origin.

BSV2 and real business data remain prohibited. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

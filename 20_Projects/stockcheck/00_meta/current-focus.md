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

SII DEV integration hardening is complete and pushed. Real SII runtime for company 1 is verified in DEV, while destructive/configurable SII regression tests are isolated to the dedicated persistent regression company.

No further SII architecture change is currently open. The next concrete StockCheck task has not yet been selected deliberately. BSV2 remains completely out of scope.

## Recently Completed

- [x] SII DEV hardening closed (`8d3884d`, `6d59b61`) — real SII runtime for company 1 verified in DEV; PFX, issued/received sync, dedupe, private R2 storage and decimal XML parsing validated; decimal parser corrected; destructive/configurable SII sync regressions isolated to persistent company 7 (`__STOCKCHECK_SII_REGRESSION__`); XML regressions safely reuse the existing company SII RUT; XML cleanup now deletes local/R2 storage objects; full `npm run build` and final `npm run test:sii` passed; real integration id 256 remained intact; no real SII call from connector unit test; BSV2 untouched.
- [x] Operational page performance optimization (`d5c40b1`)
- [x] Purchase OCR lot UX — lot/expiry capture on real Purchase before/after Apply, values survive apply/revert; OC still omits lot/expiry until conversion (`ed3b5e1`)
- [x] Sale OCR stock-origin UX + company isolation — stock-origin/batch selection on real Sale before/after Apply, FIFO fallback, selections survive apply/revert; OV omits stock origin until conversion; hardcoded companyId=1 fixed to activeCompanyId (`0b649a2`)
- [x] Pilot Session 1 completed (controlled laptop/web) — Block A: PASS. Block B: Bandeja PASS, Recetas PASS, Producción PASS, Aislamiento entre empresas PASS, Navegación simple/avanzada PASS. Mobile QA outside laptop pilot scope. BSV2 not part of this evidence. Does not imply public SaaS readiness.
  - Finding 1 — DEV role config: EXPO_PUBLIC_STOCKCHECK_ADMIN_API_KEY out of sync with backend. Resolved by synchronizing keys. DEV config issue, not a product defect.
  - Finding 2 — Purchase OCR lot UX (CLOSED, `ed3b5e1`): real Purchase now supports lot/expiry capture — values are editable before Apply, survive apply/revert. Purchase Order (OC) does NOT assign lot/expiry; lot is assigned only when OC becomes a real Purchase.
  - Finding 3 — Sale OCR stock-origin UX + company isolation (CLOSED, `0b649a2`): real Sale supports existing stock-origin/batch selection before Apply and after Apply; FIFO remains valid fallback; selections survive apply/revert. Sales Order (OV) does NOT assign stock origin; stock origin is assigned only when OV becomes a real Sale. Fixed hardcoded companyId=1 in SaleForm — now uses activeCompanyId and clears stock-origin cache on company switch.
- [x] Pilot preflight correction (`b50aaf3`) — removed remaining user-facing Business V2 / BSV2 references from DEV UI and login copy, replaced `Desarmar producto` terminology with `Revertir producción`, visually aligned the reverse-production form with current StockCheck UI, preserved production/unbuild semantics, made no API or business-logic changes, passed visual QA, passed frontend pure tests 53/53, typecheck, and static export; discovered and corrected before Pilot Session 1
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

SII DEV hardening is closed at `6d59b61` on `main` / `origin/main`. Do not reopen the completed hardening work unless new evidence appears.

Choose the next concrete StockCheck task deliberately before implementation. Analytics/Pivot Decision Support remains unstarted. Mobile QA and public SaaS remain separate concerns. BSV2 remains completely off-limits.

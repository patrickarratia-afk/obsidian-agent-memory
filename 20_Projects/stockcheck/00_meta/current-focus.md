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

Business V3 is now the current StockCheck operational test environment.

Canonical code remains `main`. `business-v3` was created directly from current `main` so the recent Odoo-like commercial, traceability, reservation, partial-delivery, production, SII and R2 improvements remain intact. BSV3 adds only reproducible local startup tooling on top of that baseline.

BSV3 runtime:
- branch: `business-v3`
- HEAD: `a101fba` (`Add reproducible Business V3 local startup`)
- remote: `origin/business-v3` at the same SHA
- backend: `http://localhost:8082`
- frontend: `http://localhost:19007`
- database: `stockcheck_business_v3`
- allowed companies: `1,2`
- permanent `.env` and `backend/.env` remain DEV and are not rewritten by the BSV3 starters

`stockcheck_business_v3` is an independent clone of the former BSV2 business database `stockcheck_business_v1`. The source BSV2 database remains untouched and backed up. BSV2 is now frozen as reference/history/backup rather than the active path.

Do not open a PR from `business-v3` to `main` by assumption. Validate BSV3 in real operational use first. If a genuinely missing BSV2 behavior is discovered later, reimplement it against modern `main`/BSV3 rather than blindly cherry-picking old BSV2 code.

## Recently Completed

- [x] Business V3 operational environment created and published (`a101fba`) — `business-v3` created directly from `main` `60f6ddf`; `stockcheck_business_v3` cloned independently from BSV2 business data; clone verified exact on core counts; all current main migrations already applied with no pending main migrations; four historical BSV2-only migration filenames retained harmlessly in migration history; copied BSV3 DB contains no SII integration config or SII sync runs; modern main backend successfully ran over cloned data; visual read-only QA passed; CORS isolated to `http://localhost:19007`; reproducible BSV3 backend/web starters added without modifying permanent DEV env files; end-to-end startup test passed with 70 products, 19 productions, HTTP 200 frontend and correct CORS; DEV `8081` remained untouched; branch pushed to `origin/business-v3`. BSV2 frozen as reference/history/backup; no PR to main yet.
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

Continue from BSV3, not BSV2.

Start BSV3 with:
- `npm run business-v3:backend`
- `npm run business-v3:web`

Then validate normal operational workflows against the cloned business data. Treat `main` as canonical code and `business-v3` as the isolated operational test branch.

Do not merge BSV3 into `main` yet. Do not modify or overwrite `stockcheck_business_v1`. Do not revive the frozen BSV2 integration branch unless new evidence requires it.

If a behavior from BSV2 appears missing during real use, inspect the modern BSV3/main implementation first and reimplement only the missing behavior if still justified. The two previously identified BSV2-only contact-lock UX guards for OV→sale and OC→purchase remain intentionally unported unless real use shows they are needed.

SII DEV hardening remains closed. Mobile QA, public SaaS readiness and Analytics/Pivot Decision Support remain separate future concerns.

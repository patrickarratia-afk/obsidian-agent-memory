---
type: context-capsule
scope: project
project: stockcheck
domain: pilot-path-qa-hardening
status: reviewed
reviewed: true
source_date: 2026-09-21
owner: patrick
aliases: [pilot-qa, pilot-hardening, pilot-path-qa]
tags: [capsule, pilot, qa, hardening]
---

# Pilot Path QA + Hardening — StockCheck Context Capsule

## Canonical Repo
`/home/patrick/Apps/Bodega V2/Bodega`

## Active Milestone
Pilot Session 1 completed for controlled laptop/web scope. Pilot Path QA + Hardening milestone formally closed in operational memory. Mobile QA remains outside this laptop pilot scope.

## Architecture Decision
Final technical review result: READY WITH CONDITIONS for a controlled laptop/web pilot. Current work is real-user pilot evidence, not speculative UI polish or a new product feature.

## Completed Sub-steps
- Pilot Session 1 completed (controlled laptop/web). Block A: PASS. Block B: Bandeja PASS, Recetas PASS, Producción PASS, Aislamiento entre empresas PASS, Navegación simple/avanzada PASS. Not public SaaS ready. BSV2 not part of this evidence.
  - Finding 1 (resolved): DEV EXPO_PUBLIC_STOCKCHECK_ADMIN_API_KEY out of sync with backend. Synchronized; role resolved as OWNER. DEV config issue, not product defect.
  - Finding 2 (resolved, `ed3b5e1`): Purchase OCR lot UX — real Purchase now supports lot/expiry capture before/after Apply; values survive apply/revert. Purchase Order (OC) does NOT assign lot/expiry; lot is assigned only when OC becomes a real Purchase.
  - Finding 3 (resolved, `0b649a2`): Sale OCR stock-origin UX + company isolation — real Sale supports existing stock-origin/batch selection before/after Apply; FIFO remains valid fallback; selections survive apply/revert. Sales Order (OV) does NOT assign stock origin; stock origin is assigned only when OV becomes a real Sale. Fixed hardcoded companyId=1 in SaleForm — now uses activeCompanyId and clears stock-origin cache on company switch.
- Current canonical commit: `0b649a2` (`Support stock origin selection for sale document lines`).
- Pilot preflight correction landed at `b50aaf3`: remaining user-facing Business V2 / BSV2 references were removed from DEV UI and login copy; `Desarmar producto` terminology was replaced with `Revertir producción`; the reverse-production form was visually aligned with current StockCheck UI; production/unbuild semantics were preserved; no API or business-logic changes were made; visual QA passed; frontend pure tests 53/53, typecheck, and static export passed.
- Purchase OCR lot UX landed at `ed3b5e1`: lot/expiry capture support on real Purchase before/after Apply with values surviving apply/revert; Purchase Order (OC) correctly omits lot/expiry until conversion.
- Sale OCR stock-origin UX + company isolation landed at `0b649a2`: stock-origin/batch selection on real Sale before/after Apply with FIFO fallback; Sales Order (OV) correctly omits stock origin until conversion; hardcoded companyId=1 in SaleForm replaced with activeCompanyId; stock-origin cache cleared on company switch.
- Final readiness evidence captured: frontend pure QA 53/53; backend pilot-critical QA previously passed in DEV; purchase/sale/stock/Kardex manual QA passed; production QA passed; company isolation QA passed; laptop visual/responsive sanity passed; performance issue fixed; cross-screen consistency passes completed; pilot preflight copy/terminology correction completed; controlled laptop/web pilot was READY WITH CONDITIONS; Pilot Session 1 completed and milestone formally closed in operational memory.
- Cross-screen consistency passes landed at `64f592b`, `8170df3`, and `993da6f`; approved visual consistency now covers Inventory, Bandeja / Incoming Documents, Ventas, Commercial / Compras-Ventas, Kardex, Production, and Recipes.
- Preserved contracts across consistency passes: mobile behavior where checked, no business logic changes, no API/SII semantics changes, and recipe behavior preserved.
- Inventory navigation performance hardening landed at `9dc60bb`; validation included 53/53 frontend pure tests, typecheck, static Expo export, and manual production-build QA at `http://localhost:8082` confirming fast navigation.
- Frontend pure QA coverage and backend pilot-critical QA landed at `e374a63`; backend DEV verification covered purchase, sale, stock/Kardex, insufficient-stock rejection, voids, production completion/void, cost handling, and write-off behavior.

## Post-pilot consolidation hardening
- Current canonical baseline: `main` `bd45ae2` / BSV3 `18c8d79`; `origin/main` matches `main`, `origin/business-v3` matches BSV3, `main` is an ancestor of BSV3, and no functional product divergence remains. BSV3 remains only an operational validation layer.
- BSV3 still uses `stockcheck_business_v3` and differs from `main` only by three runtime/config files: modified root `package.json`, `scripts/dev/start-business-v3-backend.sh`, and `scripts/dev/start-business-v3-web.sh`.
- Closed after consolidation audit: HIGH-1 sale void after customer return; MEDIUM-1 strict company context; MEDIUM-2 purchase duplicate invoice handling; MEDIUM-3A migration drift visibility/tooling; legacy converted OC receipt idempotency.
- Post-hardening consolidation audit result: **NO ACTIVE PILOT BLOCKERS FOUND**. Read-only coverage included purchases/OCs, sales/OVs, physical returns, production/unbuild, inventory/Kardex/stock origins, commercial identity, migrations/schema, company isolation, idempotency/concurrency and legacy compatibility. DTE61 return architecture and SII-primary PDF comparison remain closed.
- HIGH-2 Etiquetas remains deliberately parked as historical data: current `-1000` is explained by a continuous historical Kardex chain, but legacy origin metadata is inconsistent and no repair was requested or made. The post-hardening audit still saw product 54 stock `-1000` and did not reopen or modify it.
- DEV/BSV3 read-only invariants were clean apart from parked Etiquetas: no origin remaining greater than received, no purchase-origin/sale-origin/return-line company mismatch, and no active returns attached to voided sales or purchases.
- `SC-AUD-001` sale commercial identity hardening is CLOSED (`7278476` BSV3 → `bd45ae2` main; BSV3 resync `18c8d79`): sale POST, sale PATCH and OV→sale conversion now share duplicate identity policy for `(company_id, customer_name, document_number)` with trim-only normalization; active and voided reuse return `409 SALE_DUPLICATE`; no migration or identity canonicalization redesign was added.
- Current status: no active pilot blockers found; no known corrective integrity block from that consolidation audit is currently open; no new implementation block has been selected. HIGH-2 Etiquetas remains deliberately parked. Public SaaS readiness, mobile QA, supplier/invoice normalization and migration checksums remain separate optional/future concerns.
- These hardening fixes do not change the earlier controlled laptop/web pilot scope and do not imply public SaaS readiness; mobile QA/public SaaS readiness remain separate.

## Next Step
Pilot Session 1 closed. Next project phase undecided — decide deliberately before opening SII Integration or Analytics/Pivot implementation.

For local frontend browser QA, use `http://localhost:8082`; do not use `127.0.0.1` because backend CORS treats it as a different origin.

Do not perform more speculative UI polish before real-user evidence.

## Pilot Scope
- Laptop/web only. Mobile remains outside laptop pilot scope. Milestone formally closed in operational memory.
- Pilot used DEV/local/pilot data, backend/PostgreSQL connected, known pilot company/companies, no public SaaS assumptions.
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
Agent Memory materially reduced StockCheck context retrieval in A/B testing and should remain part of the standard StockCheck agent workflow after milestone-closing or operationally significant commits.

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

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
- HEAD: `74c16d3` (`Merge main product updates into Business V3`)
- remote: `origin/business-v3` at the same SHA
- SII real: company 1 uses `sii_direct`, validated end-to-end in BSV3
- SII runtime secrets: local ignored file `backend/.env.business-v3-sii.local`; never commit
- document storage: isolated local BSV3 root under `~/.local/share/stockcheck/business-v3/uploads`
- backend: `http://localhost:8082`
- frontend: `http://localhost:19007`
- database: `stockcheck_business_v3`
- allowed companies: `1,2`
- permanent `.env` and `backend/.env` remain DEV and are not rewritten by the BSV3 starters

`stockcheck_business_v3` is an independent clone of the former BSV2 business database `stockcheck_business_v1`. The source BSV2 database remains untouched and backed up. BSV2 is now frozen as reference/history/backup rather than the active path.

Do not bulk-merge `business-v3` into `main` by assumption. Validate changes in BSV3 first, then promote validated functional/product changes promptly and selectively to canonical `main`. Keep BSV3-only runtime/configuration out of `main`. If a genuinely missing BSV2 behavior is discovered later, reimplement it against modern `main`/BSV3 rather than blindly cherry-picking old BSV2 code.

## Main / Business V3 synchronization policy

`main` remains the canonical StockCheck product branch. `business-v3` is an operational validation environment, not an independent product line.

Any functional improvement, bug fix, API change, UI change, business rule or regression test developed and validated in BSV3 must be promoted to `main` promptly so the branches do not accumulate product divergence.

BSV3-only divergence is allowed only for environment-specific runtime/configuration such as local startup scripts, isolated ports, database selection and local secret/runtime handling.

Current synchronized baseline:
- `main`: `fa69953` (`Add inventory return workflows`)
- `business-v3`: `74c16d3` (`Merge main product updates into Business V3`)
- current BSV3-only content difference from `main`:
  - `package.json` BSV3 startup entries
  - `scripts/dev/start-business-v3-backend.sh`
  - `scripts/dev/start-business-v3-web.sh`
- current `main` is an ancestor of `business-v3`
- no functional product divergence remains after the DTE 61 Phase B2 synchronization

## Recently Completed

- [x] DTE 61 Phase B2 / Return UI + Kardex closed (`1642ece` BSV3 → `fa69953` main; BSV3 resynchronized at `74c16d3`) — added the user-facing physical-return workflow on top of the Phase B1 backend model. Venta and Compra actions now expose `Registrar devolución` for active real commercial documents; a dedicated StockCheck-styled modal distinguishes `Devolución de cliente` from `Devolución a proveedor`, prefills original document/line context, shows original / already returned / currently returnable quantities, supports Chilean decimal input, and preserves the original sale/purchase plus OV/OC quantities and allocation history. Added read-only `GET /api/inventory-returns/prepare` to resolve eligible return lines, historical sale allocations, purchase origins, existing active returns and optional same-company linked DTE 61 context without mutating stock. Single eligible origins can resolve automatically; ambiguous or split cases require explicit allocation and validate both requested totals and per-origin availability. Linked credit notes remain optional fiscal support only and never trigger stock movement automatically. Commercial Movements now shows physical-return history and refreshes immediately after a successful return. Kardex maps `devolucion_cliente` and `devolucion_proveedor` to clear user-facing labels while preserving positive Entrada vs negative Salida semantics. DTE 61 fiscal-reference reads were hardened to prefer `autoLink.reference`, then the first valid invoice reference in `references[]`, then legacy flat fields; NC 51 now shows `CodRef 3 · Ref. Factura 923 · Orden incorrecta`. Historical NC 51 / Factura 923 was reconciled operationally in BSV3 only after exact XML and Phase A candidate guards confirmed a single match; only incoming document 97 linkage/debug metadata changed and physical-return tables remained at zero, so no stock movement was created. The SII Bandeja date prefill bug was also fixed: backend timestamps such as `2026-09-17T03:00:00.000Z` are normalized to `YYYY-MM-DD`, and local calendar fallback no longer depends on UTC `toISOString()`. Manual visual QA passed for customer and supplier return flows; final validation passed `git diff --check`, TypeScript, backend build and frontend pure tests 86/86. BSV3 differs from `main` only by its three approved runtime/config files.

- [x] DTE 61 Phase B1 / physical inventory returns closed (`642fcb3` BSV3 → `a1d97bd` main; BSV3 resynchronized at `ce743e8`) — added first-class backend physical-return handling separate from DTE ingestion and separate from sale/purchase void logic. Migration `043_add_inventory_returns.sql` adds `inventory_returns`, `inventory_return_lines` and `inventory_return_line_allocations`; customer returns create positive `devolucion_cliente` stock movements and restore the exact original tracked stock origin when available, while legacy/null-origin sale stock is returned without fabricating an origin; supplier returns create negative `devolucion_proveedor` movements against exact remaining purchase origins and mark an origin depleted at zero. Multiple partial returns are cumulative; ambiguous multi-origin cases require explicit allocation and never guess. Original sale/purchase status and quantities, `sale_line_stock_origins`, OV delivered quantities and OC received quantities remain unchanged. An optional linked DTE 61 may support a return only when it belongs to the same company/type/original entity; a credit note by itself never changes stock. Added `POST/GET /api/inventory-returns`, exact `stock_movement_origins` traceability, audit event `inventory_return.created`, schema coverage and a dedicated regression suite hardened to run only against `stockcheck_dev`. The regression covers tracked, legacy, partial, cumulative, multi-origin, wrong-origin, DTE-link and company-isolation cases and asserts TAG cleanup. Validation passed build, schema, sale/purchase, void, manual-batch, write-off, SII auto-link and inventory-return tests. Migration 043 was then applied transactionally to operational `stockcheck_business_v3`; the three new return tables were empty immediately after migration and operational counts remained exactly unchanged: sales 44, purchases 34, stock movements 380, stock origins 64, products 71 and total product stock 724.00.

- [x] DTE 61 Phase A synchronized (`271a506` BSV3 → `b68d09d` main; BSV3 resynchronized at `aca741e`) — added typed parsing of one or multiple SII `<Referencia>` blocks with raw `TpoDocRef`, `FolioRef`, `FchRef`, `CodRef` and `RazonRef`; added a separate deterministic DTE 61 auto-link path that links issued credit notes to the referenced sale and received credit notes to the referenced purchase using company + direction + referenced invoice folio + counterparty RUT + non-voided original, intentionally without requiring total equality because credit notes may be partial; existing DTE 33 exact-match auto-link behavior remains unchanged; no sale/purchase creation, voiding, original-total mutation, delivered/received quantity change or stock movement is performed by DTE 61 ingestion; `SiiDteViewerModal` now shows compact invoice-reference / correction-code / reason information and Commercial Movements can surface linked `NC <folio>` as a secondary SII document while preserving the invoice as primary. No migration was required; existing `incoming_documents`, `linked_entity_type/id` and `extraction_debug` are reused. Real read-only BSV3 validation found NC 51 referencing Factura 923 and exactly one sale candidate (sale 75); the already-imported NC 51 remains historically unlinked because Phase A intentionally avoided operational DB backfill. Validation passed parser tests, SII auto-link regressions including no-stock checks, `git diff --check`, TypeScript and frontend pure tests 69/69. Odoo Community remains a conceptual reference for separating financial credit-note reversal from physical stock return, not a source for blindly copied implementation code.

- [x] Commercial document workflows synchronized (`1892529` BSV3 → `e23e65a` main; BSV3 resynchronized at `a054362`) — fixed Commercial Movements Actions first-click behavior by conditionally mounting commercial action modals, matching the proven Production modal pattern; modernized Editar datos consistently for Compra, Venta, OC and OV; separated official SII/XML from commercial Factura PDF/JPG and other attachments; added Factura as a supported attachment type plus explicit attachment-type reclassification without re-uploading or duplicating storage; unified invoice resolution so either a primary PDF/JPG or an attachment typed `invoice` is treated as the commercial invoice while XML SII never is; invoice attachments are excluded from Otros respaldos and coexist cleanly with linked SII; PurchaseForm and SaleForm allow selecting commercial invoice PDF/JPG while preserving `incomingDocumentId`; Commercial Movements displays only `Factura SII` when SII is the sole document and `Factura` + secondary `SII` when a commercial invoice also exists; Venta table header is now `Factura` and shows only `sale.document_number`; Inventory no longer renders SKU beneath product names while SKU search remains active; Bandeja SII sync-result messaging was aligned visually with StockCheck; textarea notes visual clipping was corrected; OV administrative editing uses the sales-order endpoint rather than the sale endpoint. Manual QA included Urzken invoice 32882 reclassification from Otro to Factura. A final micro-adjustment centered the Venta `Factura` header and invoice numbers (`47564f7` BSV3 → `3949fa5` main; BSV3 resynchronized at `534fba8`). Final validation passed `git diff --check`, TypeScript and frontend pure tests 68/68.

- [x] SII document + Operational Expenses UX synchronized (`0466d92` BSV3 → `e050b0b` main; BSV3 resynchronized at `8ca0a72`) — extracted the readable SII DTE invoice UI into shared `SiiDteViewerModal`; Bandeja, Commercial Movements and Operational Expenses now reuse the same official-XML-backed readable viewer; Commercial Movements distinguishes normal `Factura` from `Factura SII` / `SII`, preserving the original XML as a secondary action inside the viewer; Operational Expenses gained the same SII behavior, a denser ERP-style table, consistent StockCheck controls/status badges, Inventory-style single scroll viewport/sticky behavior, and a unified compact New/Edit/Classify-from-Bandeja form. Visual design work uses Odoo as a reference for ERP ideas and workflows, but existing StockCheck screens/components remain the primary visual consistency reference. Manual visual QA passed; `git diff --check`, TypeScript and frontend pure tests 57/57 passed.
- [x] Production completion/actions UX synchronized (`36f31e4` BSV3 → `91c858a` main; BSV3 resynchronized at `42f4e93`) — production no longer blocks completion with false `Envase: falta 0 unidades` rows when required container quantity is zero; Production History Actions modal now mounts only when a record exists so Actions opens immediately without requiring a page refresh. Manual BSV3 QA passed; TypeScript and frontend pure tests 57/57 passed.
- [x] Historical BSV3 document-storage recovery pass completed — audited 134 company-1 document references and restored 27 missing physical paths from verified Google Drive originals without changing database rows. Post-restore audit leaves 8 missing references representing 7 unique unresolved files: Servicios Blue Mountains invoice 869; Sodimac purchase dated 2026-06-24; Deter Center invoice 11126 (same physical file referenced by purchase + manual Bandeja row); and POD attachments for sales 876, 880, 907 and 917. All known SII XML files remained physically present. Do not substitute unrelated files or rewrite DB references to hide these missing originals.

- [x] BSV3 SII document UX + auto-link V1 closed (`46bf164`, `89b178b`, `ecbcf0e`, `55a340c`, `350e9db`) — configured BSV3 document storage is now served from the isolated runtime root; DTE parsing preserves line units and additional taxes; a read-only SII DTE summary endpoint and human-readable invoice viewer were added while retaining the official XML unchanged; new DTE type 33 documents auto-link only to an existing exact sale/purchase match on company + direction + folio + normalized counterparty RUT + exact gross total + non-voided status; ambiguous, missing or unsupported matches remain extracted; duplicate SII identities remain idempotent and are never relinked on re-import; candidate resolution, row lock, incoming-document insert and audit log are protected in one transaction; regression coverage runs against `stockcheck_dev` company 7 and confirms no sale, purchase, line or stock movement is created by linking. Historical BSV3 reconciliation completed: incoming 82→sale 74, 83→sale 72, 84→sale 71, 85→sale 73; manual incoming 81 also remains linked to sale 74; incoming 86–89 remain extracted with zero exact purchase candidates. Company 1 core counts after closeout remain purchases 33, purchase_lines 70, sales 42, sale_lines 192, stock_movements 371, incoming_documents 59.
- [x] BSV3 real SII operational validation (`0b7f58b`) — BSV3 backend starter now requires and loads the ignored local SII runtime secret file; `NODE_ENV=production`, live SII enablement, PFX presence/password and isolated local document storage are validated before startup; real `sii_direct` integration configured for company 1 / RUT 76337063-1 through the official API; first real both-direction sync succeeded with 8 documents created, 0 duplicates ignored and 0 failures; 8 XML files stored in the isolated BSV3 document root; second sync succeeded with no documents to process and left SII document count, max incoming-document ID and physical-file count unchanged, confirming safe repeat execution; DEV remained untouched on 8081. Historical cloned document storage audited: 45/50 manual-upload files recovered and copied with SHA-256 equality; 5 source files are physically missing locally (incoming IDs 77–81, including manual PDFs 919–922); no DB rows were rewritten and no XML was substituted for missing manual originals. Historical manual/SII overlap for invoice 922 was reconciled safely: manual incoming 81 and SII incoming 82 both link to sale 74 without creating a duplicate sale or stock movement.
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
- [x] Agent Memory scaffold created for StockCheck

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

Current synchronized code baseline:
- canonical `main`: `fa69953`
- operational `business-v3`: `74c16d3`
- BSV3-only content difference remains limited to `package.json` startup entries plus `scripts/dev/start-business-v3-backend.sh` and `scripts/dev/start-business-v3-web.sh`
- `main` is an ancestor of `business-v3`; no functional product divergence remains
- BSV3 database has migration `043_add_inventory_returns.sql` applied and the physical-return UI/Kardex workflow is implemented and validated

BSV3 remains the primary operational validation environment with real SII connectivity.

Commercial document handling is now closed for the current scope:
- Compra / Venta / OC / OV administrative edit flows share the modern StockCheck visual language
- official SII XML is distinct from commercial Factura PDF/JPG
- commercial invoices can come from the primary document or an attachment typed `invoice`
- invoice attachments do not remain duplicated under Otros respaldos
- attachments can be explicitly reclassified without re-uploading the file
- Commercial Movements shows `Factura`, `Factura SII`, or `Factura` + `SII` according to document availability
- Venta table shows only the invoice/document number in its Factura column
- Inventory hides SKU in the table while keeping SKU searchable
- commercial Actions should open on first click without page refresh

For future ERP/product UX work, use Odoo as a useful reference for workflows, information hierarchy and mature ERP patterns, but do not copy Odoo blindly. Existing StockCheck screens, primitives, spacing, table behavior and interaction patterns remain the primary source of visual consistency.

## Current Product Focus

DTE 61 Phase A, Phase B1 and Phase B2 are now closed and synchronized.

Current return architecture:
- DTE 61 / Nota de crédito is fiscal evidence and optional supporting context only
- physical stock movement requires an explicit StockCheck return operation
- customer returns restore stock through `devolucion_cliente`
- supplier returns consume stock through `devolucion_proveedor`
- single-origin cases may resolve deterministically; ambiguous multi-origin cases require explicit allocation
- partial and repeated returns are supported without voiding or destructively rewriting the original sale/purchase
- Commercial Movements shows return history and Kardex shows the resulting physical movement
- original invoice, sale/purchase, OV/OC delivery/receipt quantities and original allocation history remain intact
- CodRef 1/2/3 never causes automatic physical stock movement

Real BSV3 fiscal reconciliation:
- NC 51 is linked to sale 75 / Factura 923
- fiscal context: `CodRef 3 · Ref. Factura 923 · Orden incorrecta`
- this historical reconciliation changed only the incoming-document linkage/debug metadata
- no `inventory_returns`, return lines, return allocations or stock movements were created by that reconciliation

The next product implementation block has not yet been selected. Continue from current BSV3/main rather than reopening BSV2 or extending DTE 61 by assumption.

Known historical document-storage gap remains: 8 broken references / 7 unique missing originals after the recovery pass (Blue Mountains 869, Sodimac 2026-06-24, Deter Center 11126, POD 876/880/907/917). Do not modify database references or substitute unrelated files merely to eliminate these missing-file indicators.

Do not bulk-merge BSV3 runtime/configuration into `main`. Keep the environment-specific BSV3 layer separate. Do not modify or overwrite `stockcheck_business_v1`. Do not revive the frozen BSV2 integration branch unless new evidence requires it.

If a behavior from BSV2 appears missing during real use, inspect the modern BSV3/main implementation first and reimplement only the missing behavior if still justified. The two previously identified BSV2-only contact-lock UX guards for OV→sale and OC→purchase remain intentionally unported unless real use shows they are needed.

SII DEV hardening remains closed. Mobile QA, public SaaS readiness and Analytics/Pivot Decision Support remain separate future concerns.

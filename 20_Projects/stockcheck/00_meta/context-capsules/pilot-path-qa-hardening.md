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
Pilot Path QA + Hardening is the current engineering milestone after Pilot Onboarding + Simple Mode Readiness (`324afd6`).

## Architecture Decision
StockCheck is ready with conditions for a controlled accompanied pilot. Current engineering work is QA/hardening, not a new product feature.

## Completed Sub-steps
- Cross-screen consistency pass 1 landed at `64f592b` (`Align documents workspace with inventory`).
- Inventory micro-polish: header top spacing was slightly increased; density/table layout unchanged.
- Incoming Documents / Bandeja redesign: compact page header, primary `+ Documento`, grouped SII actions, compact search/summary, preserved status/target filters, and table visually/behaviorally aligned with Inventory.
- Documents preserved UI contracts: one horizontal scrollbar, visible vertical scrollbar, frozen Proveedor / N° doc. / Fecha columns, preserved header/data alignment, and verified mobile behavior.
- Visual QA passed; no business logic changes and no API/SII semantics changed.
- Inventory visual redesign landed at `2f37b16` (`Redesign inventory workspace`).
- Inventory is now denser and table-first: `Inventario` is the primary header anchor; search is closer to title/content; actions and summary are compact; filters and sort share a compact toolbar; the table starts materially higher and consumes more viewport.
- Preserved UI contracts: frozen Product column, horizontal scroll, one visible horizontal scrollbar at the bottom of the table viewport, visible vertical scrollbar, aligned headings/data, and mobile behavior.
- Preserved performance boundaries: `React.memo(HomeInventoryView)`, stable `HomeScreen` props, memoized Maps, cached formatters, no virtualization, and no backend/business logic changes; visual QA passed.
- Inventory navigation performance hardening landed at `9dc60bb` (`Improve inventory navigation performance`).
- Manual QA had found a consistent ~2 second delay opening Compra, Venta, Bandeja, Más, and other screens.
- Root cause: `HomeInventoryView` was always mounted; unrelated `HomeScreen` state changes caused full inventory rerenders; roughly 800 products rendered in duplicated frozen/scrollable table structure; `Intl.NumberFormat` objects were repeatedly created per row/cell; committed/expected maps were rebuilt repeatedly; unstable props prevented the memo boundary.
- Fix: cached `Intl.NumberFormat` formatters; added `React.memo` to `HomeInventoryView` with default shallow comparison; stabilized `HomeInventoryView` props/callbacks; removed unused unstable props; memoized committed/expected maps.
- Validation: 53/53 frontend pure tests passed, typecheck passed, static Expo export passed, manual production-build test at `http://localhost:8082` confirmed navigation is fast again, business behavior unchanged, navigation semantics unchanged, repo clean after commit/push.
- Frontend pure QA coverage landed at `e374a63` (`Add pilot frontend pure QA tests`).
- Coverage includes importer helpers and pilot readiness X/4 logic.
- Verification captured: 53 frontend pure tests passed, typecheck passed, Node built-in `node:test` runner, no new test dependency.
- Backend pilot-critical QA passed at `e374a63` against confirmed DEV database `stockcheck_dev` using `backend/npm run test:pilot-critical`.
- Backend verification covered build, audit logs, manual stock batches, purchase flow, sale flow, insufficient stock rejection, void sale, production completion, void production, and stock write-off.
- Verified business behavior: purchases increase stock with Kardex/origin records; sales reduce FIFO stock with traceability; insufficient stock blocks sale without mutation; void sale restores stock and origin traceability; planned production does not move stock; completed production consumes materials and creates finished stock; production cost calculation/override works; void production reverses stock; write-off consumes FIFO/manual origins and records Kardex.
- Post-test state: git working tree clean, HEAD remained `e374a63`, and tests produced no code changes.

## Next Step
Cross-screen consistency next priority: Ventas focused redesign.

After that: Commercial / Kardex / Production / Recipes small polish.

For local frontend browser QA, use `http://localhost:8082`; do not use `127.0.0.1` because backend CORS treats it as a different origin.

Do not mark Pilot Path QA + Hardening complete until manual browser QA is done.

## Safety Boundary
BSV2 and real business data are completely off-limits. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

## Known Non-blocking Issue
`splitCsvLine` has a pre-existing CSV edge case where quoted empty fields can parse incorrectly. Do not promote it to a blocker unless later QA proves impact.

## Operational Memory Note
Obsidian materially reduced StockCheck context retrieval in A/B testing and should remain part of the standard StockCheck agent workflow after milestone-closing or operationally significant commits.

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

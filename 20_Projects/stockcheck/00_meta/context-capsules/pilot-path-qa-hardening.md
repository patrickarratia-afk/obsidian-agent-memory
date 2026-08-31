---
type: context-capsule
scope: project
project: stockcheck
domain: pilot-path-qa-hardening
status: active
reviewed: false
source_date: 2026-08-31
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
Manual browser QA is expected for onboarding/readiness X/4, manual product creation, CSV/XLS/XLSX import, duplicate behavior, purchase, sale, insufficient-stock UX, Kardex/traceability, incoming documents, company switching/isolation, Modo simple / Avanzado navigation, laptop layout, and mobile layout.

For local frontend browser QA, use `http://localhost:8082`; do not use `127.0.0.1` because backend CORS treats it as a different origin.

Inventory page needs a separate focused visual redesign using `design-md`: reduce blank vertical space, move search closer to title/table, reduce filters/order height, bring the table higher, and make inventory denser and more table-first.

Do not mark Pilot Path QA + Hardening complete until manual browser QA is done.

## Safety Boundary
BSV2 and real business data are completely off-limits. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

## Known Non-blocking Issue
`splitCsvLine` has a pre-existing CSV edge case where quoted empty fields can parse incorrectly. Do not promote it to a blocker unless later QA proves impact.

## Operational Memory Note
Obsidian materially reduced StockCheck context retrieval in A/B testing and should remain part of the standard StockCheck agent workflow after milestone-closing or operationally significant commits.

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

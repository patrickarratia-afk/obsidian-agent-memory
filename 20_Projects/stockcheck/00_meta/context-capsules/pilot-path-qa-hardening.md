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
- Frontend pure QA coverage landed at `e374a63` (`Add pilot frontend pure QA tests`).
- Coverage includes importer helpers and pilot readiness X/4 logic.
- Verification captured: 53 frontend pure tests passed, typecheck passed, Node built-in `node:test` runner, no new test dependency.
- Backend pilot-critical QA passed at `e374a63` against confirmed DEV database `stockcheck_dev` using `backend/npm run test:pilot-critical`.
- Backend verification covered build, audit logs, manual stock batches, purchase flow, sale flow, insufficient stock rejection, void sale, production completion, void production, and stock write-off.
- Verified business behavior: purchases increase stock with Kardex/origin records; sales reduce FIFO stock with traceability; insufficient stock blocks sale without mutation; void sale restores stock and origin traceability; planned production does not move stock; completed production consumes materials and creates finished stock; production cost calculation/override works; void production reverses stock; write-off consumes FIFO/manual origins and records Kardex.
- Post-test state: git working tree clean, HEAD remained `e374a63`, and tests produced no code changes.

## Next Step
Manual browser QA is expected for onboarding/readiness X/4, manual product creation, CSV/XLS/XLSX import, duplicate behavior, purchase, sale, insufficient-stock UX, Kardex/traceability, incoming documents, company switching/isolation, Modo simple / Avanzado navigation, laptop layout, and mobile layout.

Do not mark Pilot Path QA + Hardening complete until manual browser QA is done.

## Safety Boundary
BSV2 and real business data are completely off-limits. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

## Known Non-blocking Issue
`splitCsvLine` has a pre-existing CSV edge case where quoted empty fields can parse incorrectly. Do not promote it to a blocker unless later QA proves impact.

## Operational Memory Note
Obsidian materially reduced StockCheck context retrieval in A/B testing and should remain part of the standard StockCheck agent workflow after milestone-closing or operationally significant commits.

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

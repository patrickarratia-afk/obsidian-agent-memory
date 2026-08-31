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

## Completed Sub-step
- Frontend pure QA coverage landed at `e374a63` (`Add pilot frontend pure QA tests`).
- Coverage includes importer helpers and pilot readiness X/4 logic.
- Verification captured: 53 frontend pure tests passed, typecheck passed, Node built-in `node:test` runner, no new test dependency.

## Next Step
Run the existing backend pilot-critical test suite against DEV only: `stockcheck_dev`.

`test:pilot-critical` is DEV-mutating and has not yet been executed in this milestone.

## After Backend Tests
Manual browser QA is expected for onboarding/readiness X/4, product create/import, purchase, sale, Kardex/traceability, incoming documents, company switching/isolation, Modo simple / Avanzado navigation, and laptop/mobile sanity.

## Safety Boundary
BSV2 and real business data are completely off-limits. Do not connect to, inspect, query, mutate, or use BSV2 for QA evidence.

## Known Non-blocking Issue
`splitCsvLine` has a pre-existing CSV edge case where quoted empty fields can parse incorrectly. Do not promote it to a blocker unless later QA proves impact.

## Operational Memory Note
Obsidian materially reduced StockCheck context retrieval in A/B testing and should remain part of the standard StockCheck agent workflow after milestone-closing or operationally significant commits.

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

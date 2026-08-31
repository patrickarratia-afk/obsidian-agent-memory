---
type: context-capsule
scope: project
project: stockcheck
domain: pilot-onboarding-readiness
status: active
reviewed: false
source_date: 2026-08-31
owner: patrick
aliases: [pilot-readiness, onboarding-readiness, product-readiness]
tags: [capsule, pilot, onboarding, readiness]
---

# Pilot Onboarding Readiness — StockCheck Context Capsule

## Canonical Repo
`/home/patrick/Apps/Bodega V2/Bodega`

## Milestone
Pilot Onboarding + Simple Mode Readiness completed in commit `324afd6` (`Add pilot onboarding readiness`).

## Readiness Model
- Pilot readiness is progress-aware.
- Readiness denominator is X/4:
  1. real/non-template product exists
  2. non-voided purchase exists
  3. non-voided sale exists
  4. incoming document exists
- Informational, session, and optional steps do not count toward X/4.
- Review viewed state is session-only and resets on company switch.
- Incoming-document readiness is isolated across company switches with stale-request protection.

## UX Boundary
- Existing "Modo simple" / "Avanzado" grouping remains.
- No simple-mode toggle was introduced.

## Importer Boundary
- CSV/XLS/XLSX importer preflights duplicates within the uploaded file and against loaded existing products by normalized SKU/name.
- Valid nonduplicate rows continue importing.
- Backend `PRODUCT_DUPLICATE` 409 fallback remains.

## Preserved Contracts
- No backend changes.
- No hooks changes.
- No type changes.
- No design-system changes.

## Review Evidence
Final independent GPT-5.5 review passed after focused fixes.

## Deeper Context
- `.project-wiki/implementation/current-plan.md`
- `.project-wiki/STATUS.md`
- `src/components/HomeGuidePage.tsx`
- `src/screens/HomeScreen.tsx`
- `src/screens/ProductCsvImportModal.tsx`

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

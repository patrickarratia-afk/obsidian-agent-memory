---
type: context-capsule
scope: project
project: stockcheck
domain: frontend-redesign
status: active
reviewed: false
source_date: 2026-08-30
owner: patrick
aliases: [frontend-redesign, frontend-phase]
tags: [capsule, frontend, redesign]
---

# Frontend Redesign — StockCheck Context Capsule

## Canonical Repo
`/home/patrick/Apps/Bodega V2/Bodega`

## Objective
Systematic polish of all StockCheck screens toward a calm, modern-operational, dense table-first enterprise UI.

## Completed Phases

| Phase | Scope | Git Ref | Date |
|-------|-------|---------|------|
| 1 | Design system foundations — `src/ui/tokens.ts`, `src/ui/primitives.tsx`, refined `HomeInventoryView`, `ProductionActionsSheet` | `af5de16` | 2026-08-30 |
| 2 | App shell + inventory workspace — `HomeScreen.styles.ts`, refined `HomeInventoryView` | `d90d287` | 2026-08-30 |
| 3 | Product Detail + Kardex — full rewrite of `ProductDetailPage.tsx` | `f713a46` | 2026-08-30 |
| 4 | Commercial — `CommercialMovementsPage`, `PurchaseForm`, `SaleForm`, `CommercialFormModals`, `CommercialActionModals`, `ActualSaleActionsSheet`, `SalesPlanningActionsSheet` | `98754d1` | 2026-08-30 |

## Phase 4 Summary
- Adopted `tablePrimitiveStyles`, `StatusBadge`, `AppButton`, `actionSheetPrimitiveStyles`, `modalPrimitiveStyles` across all 7 commercial surfaces
- Replaced ~60 hardcoded hex values with design tokens
- All business logic, OCR, document upload, line management, stock-origin allocation, order-to-document conversion, void flows preserved
- Final focused review passed; no backend/API/hooks modified

## Design System
- **Palette**: calm teal primary (`#1F6F78`), neutral backgrounds (`#F5F7F8`), subtle borders (`#DDE5E8`)
- **Typography**: compact (`tableBody: 12px`, `tableHeader: 11px`), pragmatic
- **Spacing**: tight (`pageGutter: 16`, `sectionGap: 12`, `tableRowMinHeight: 44`)
- **Primitives**: `StatusBadge`, `AppButton`, `tablePrimitiveStyles`, `modalPrimitiveStyles`, `actionSheetPrimitiveStyles`
- **Direction**: maintain AGENTS.md UX rules — compact tabs, stable layout, module-grouped actions, Chilean locale

## Next Phase
**Production** — production forms, completion modal, unbuild modal, production history page, recipes.

## Deferred / Out of Scope
- Backend architecture decomposition
- SII, documents, reports, admin screens
- Automated frontend tests
- BSV2 — completely off-limits

## Validation
Frontend changes follow AGENTS.md UX checklist. Backend flow tests verify business outcomes. Verify visually on web (`npm run dev:web`).

## Deeper Context
- `.project-wiki/technical/modules/frontend-application-shell.md`
- `.project-wiki/technical/modules/inventory-commercial-workflows.md`
- `.project-wiki/technical/modules/production-workflows.md`
- `.project-wiki/technical/codebase-map.md`
- `AGENTS.md`
- `src/ui/tokens.ts`
- `src/ui/primitives.tsx`

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

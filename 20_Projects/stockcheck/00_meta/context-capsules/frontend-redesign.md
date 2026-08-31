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
| 3 | Product Detail + Kardex — full rewrite of `ProductDetailPage.tsx` (+628/-212) | `f713a46` | 2026-08-30 |

## Design System
- **Palette**: calm teal primary (`#1F6F78`), neutral backgrounds (`#F5F7F8`), subtle borders (`#DDE5E8`)
- **Typography**: compact (`tableBody: 12px`, `tableHeader: 11px`), pragmatic
- **Spacing**: tight (`pageGutter: 16`, `sectionGap: 12`, `tableRowMinHeight: 44`)
- **Primitives**: StatusBadge (soft/outline tones), DataTable, Modal, ActionSheet, filter/chip bars
- **Direction**: maintain AGENTS.md UX rules — compact tabs, stable layout, module-grouped actions, Chilean locale (`dd/mm/yyyy`, CL number format)

## Next Phase
**Commercial** — purchase forms, sale forms, commercial movements page, purchase/sales orders, partial delivery/receipt surfaces.

## Deferred / Out of Scope
- Backend architecture decomposition (large `server.ts` stays as-is)
- Production, SII, documents, reports, admin screens — not yet prioritized for redesign
- Automated frontend tests (backend flow tests cover API-level outcomes)
- BSV2 — completely off-limits

## Validation
Frontend changes follow AGENTS.md UX checklist. Backend flow tests verify business outcomes. No frontend test suite exists — verify visually on web (`npm run dev:web`).

## Deeper Context
- `.project-wiki/technical/modules/frontend-application-shell.md` — app shell docs
- `.project-wiki/technical/modules/inventory-commercial-workflows.md` — commercial domain context
- `.project-wiki/technical/codebase-map.md` — full source tree
- `AGENTS.md` — UX/UI design rules (authoritative)
- `src/ui/tokens.ts` — design tokens
- `src/ui/primitives.tsx` — UI primitives

## Authority
Repo/tests > Project Wiki > this capsule. If repo state contradicts this capsule, update here.

---
type: log
scope: global
status: active
reviewed: true
tags: [log, system]
---

# Vault Changes

Log significant structural changes to the vault here. Minor edits to notes do not need to be recorded.

| Date | Change | Actor |
|------|--------|-------|
| 2026-04-19 | Initial vault scaffold created from obsidian-agent-memory template | — |
| 2026-08-30 | Adapted vault for StockCheck project — updated RETRIEVAL_PROTOCOL, SESSION_CLOSEOUT_PROTOCOL, created stockcheck project folder with _project.md, current-focus.md, project-wiki-bridge.md, context-capsules/README.md | Codex |
| 2026-08-31 | Created StockCheck Pilot Path QA + Hardening context capsule | Hermes Agent |

## 2026-09-01 — PoolCheck operational memory added

- Added `20_Projects/poolcheck/` using the canonical project template.
- Added PoolCheck `_project.md`.
- Added `00_meta/current-focus.md`.
- Added `00_meta/project-wiki-bridge.md`.
- Configured Hermes `OBSIDIAN_VAULT_PATH` to the shared operational vault.
- No PoolCheck Project Wiki existed at setup time; bridge records this explicitly.

## 2026-09-01 — PoolCheck Project Wiki activated

- Confirmed canonical `.project-wiki/` at `/home/patrick/Apps/PoolCheck`.
- Project Wiki uses schema `project-wiki 1.4.0`.
- Canonical deterministic validation passed with 0 errors and 0 warnings.
- Updated PoolCheck Project Wiki bridge and operational retrieval path.
- Current implementation focus remains P1 7E-B — Facility Management UI.

## 2026-09-01 — PoolCheck P1 7E-B closed

- Facility Management UI for owner admins completed and pushed.
- Canonical PoolCheck HEAD: `7e1347c Add facility management UI`.
- `/facilities` now supports admin-only list/create/edit/delete management.
- `FACILITY_IN_USE` is handled without losing delete-dialog context.
- Pool → Facility assignment UI remains the next product objective; exact slice label must be confirmed from current Project Wiki/repo before implementation.
- Project Wiki remains canonical and validates with 0 errors / 0 warnings.
- No backend, OpenAPI, generated-client, database, or migration changes were part of 7E-B.

## 2026-09-01 — PoolCheck P1 7E-C closed

- Owner-side Pool → Facility assignment workflow completed and pushed.
- Canonical PoolCheck HEAD: `bec57bc Add pool facility assignment UI`.
- Pool creation now supports Facility assignment.
- Existing Pools can assign, move, and detach from Facilities.
- Provider-portfolio cache invalidation is included after Pool creation and Facility assignment changes.
- Provider Facility management and Facility grants remain out of scope/unimplemented.
- Project Wiki validates with 0 errors / 0 warnings.
- No backend, OpenAPI, generated-client, database, migration, or test changes were part of 7E-C.
- Project is paused pending confirmation of the next canonical product slice.

## 2026-09-02 — PoolCheck P1 delegated maintenance/backwash closed

- Canonical PoolCheck HEAD: `04765c6 Add delegated maintenance and backwash UI`.
- Provider delegated Pool workspace now supports maintenance and filter-backwash history plus capability-gated creation.
- Maintenance creation remains gated by provider role semantics plus `canMaintain`.
- Backwash creation remains gated by provider role semantics plus `canBackwash`.
- Delegated maintenance photo evidence is intentionally hidden because current maintenance-photo endpoints remain owner-scoped.
- Provider planned-work execution is intentionally disabled in the reused backwash component for this slice.
- Existing owner photo evidence and planned-work behavior remain unchanged.
- No backend, OpenAPI, generated-client, database, schema, or migration changes were made.
- Project Wiki validates with 0 errors / 0 warnings.
- Remaining P1 roadmap work is explicitly retained: corrective-action/verification, provider dosage, and cross-org planned work/provider-member assignment where justified.
- Provider Facility management and Facility grants/inheritance remain unresolved/deferred.
- Project is paused before selecting/starting the next canonical slice.

## 2026-09-02 — PoolCheck Provider Corrective Actions + Verification UI closed

- Canonical PoolCheck HEAD: `2fccccf Add delegated corrective action verification UI`.
- Delegated corrective-action history, admin management (mark applied / dismiss), and admin verification UI implemented frontend-only on provider Pool detail.
- Non-admin users remain read-only even if capability flags exist; backend remains final authorization authority.
- Manual measurement ID fallback added with strict canonical safe-integer validation.
- OUT_OF_RANGE_EFFECTIVE_CONFIRMATION_REQUIRED two-step confirmation maintained.
- Provider corrective creation, recommendations, apply-product, dosage, backend/API changes, and Facility changes explicitly excluded from this slice.
- No raw grant/relationship IDs exposed; GPT-5.5 final commit-gate passed with FINDINGS NONE.
- Existing delegated backend corrective/verification integration coverage already exists — frontend-only slice, integration not required.
- Durable model-routing workflow and skill routing rules recorded in `_project.md`.
- UI/UX audit planned as next quality milestone (GPT-5.5, read-only).

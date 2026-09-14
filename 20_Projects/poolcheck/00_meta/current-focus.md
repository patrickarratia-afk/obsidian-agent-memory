---
type: reference
scope: project
project: poolcheck
status: active
reviewed: true
tags: [focus, active]
---

# Current Focus — PoolCheck

## Canonical Baseline

Branch: `main`

Repository HEAD:

`506392c Sync PoolCheck project wiki with current state`

Latest product/code HEAD:

`a1790db Fix measurement chart chronological order`

The `506392c` commit updates Project Wiki documentation only. Product/code state remains represented by `a1790db`.

Working tree was clean after the Project Wiki synchronization commit on 2026-09-14.

## Recently Completed

- [x] Facility foundation — Organization → Facility → Pool
- [x] Facility CRUD API and Pool assignment contract
- [x] Facility-aware Pool filtering
- [x] Provider Facility portfolio enrichment/filter
- [x] Provider operational-status enrichment/filter
- [x] Canonical Project Wiki 1.4.0 installed and validated (0 errors / 0 warnings)
- [x] Delegated Maintenance & Backwash Provider UI
- [x] Provider Corrective Actions + Verification UI

P1 portfolio filtering dimensions now covered:

- client / organization
- Facility
- Pool/search
- operational status

## Current Objective

No product feature is currently active.

PoolCheck knowledge and routing synchronization was completed and validated on 2026-09-14:

- Project Wiki synchronized in repository commit `506392c`
- Agent Memory synchronized in commit `dbedba3`
- Hermes Projects `poolcheck` activated as routing-only project
- `poolcheck-development` skill routes through Hermes Projects → Agent Memory → Project Wiki / repository
- Telegram routing validation confirmed the canonical paths and authority order
- PatrickA Obsidian is outside the normal canonical PoolCheck routing path

The next previously planned quality milestone remains a separate full PoolCheck UI/UX audit, but it is not started and must not be launched automatically.

Do not start product features by assumption. Confirm current human direction first.

## Post-Corrective Operational Milestones

Verified committed state after `2fccccf`:

- `8133b30` — safe tracked database migration workflow
- `23811aa` — delegated provider dosage
- `01609b7` — delegated Pools on operational dashboard
- `ccf7629` — delegated technician restrictions
- `3a0cfc4` — delegated Pool trends and combined chlorine
- `0a103a1` — scoped operational Pool reports
- `3e7c11d` — delegated Pool detail hook-order fix
- `a1790db` — measurement chart chronological-order fix
- `506392c` — Project Wiki synchronized to current repository state

## Explicitly Deferred

Current unresolved/deferred product areas:

- cross-org planned work / provider-member assignment where justified
- provider Facility management
- Facility grants/inheritance

Do not start these by assumption. Confirm current product and authorization direction first.

## Known Non-Blocking Technical Debt

Provider portfolio operational-status enrichment currently performs one latest-measurement lookup per authorized Pool.

This N+1 behavior passed review and is intentionally deferred unless real portfolio scale makes batching necessary.

## Workflow

For significant changes:

1. inspect
2. discuss
3. decide
4. implement
5. validate
6. review diff/status
7. commit when explicitly authorized
8. push when explicitly authorized
9. update operational memory only for meaningful milestones/decisions
10. close

Do not repeat already-closed audits without new evidence.


## Latest Milestone Closure — P1 7E-B

- [x] Facility Management UI for owner admins completed.
- [x] `/facilities` route added.
- [x] Admin-only `Instalaciones` navigation added.
- [x] Non-admin direct navigation protected with restricted state.
- [x] Facility list, create, rename/edit, and delete UI implemented.
- [x] `FACILITY_IN_USE` handled with friendly inline feedback.
- [x] Pool → Facility assignment UI intentionally remains unimplemented.
- [x] Provider Facility management remains deferred.
- [x] GPT-5.5 final commit-gate: FINDINGS NONE / READY TO COMMIT.
- [x] Project Wiki validator: valid=true, errors=0, warnings=0.
- [x] Frontend typecheck, PoolCheck typecheck, and build passed.
- [x] Integration suite was not run because `TEST_DATABASE_URL` was unavailable; accepted as non-blocking because 7E-B changed no backend/API/DB/generated code.
- [x] Commit pushed: `7e1347c Add facility management UI`.

## Latest Milestone Closure — P1 7E-C

- [x] Owner-side Pool → Facility assignment UI completed.
- [x] Pool creation supports Facility assignment.
- [x] Existing Pools can be assigned to a Facility.
- [x] Existing Pools can move between Facilities.
- [x] Existing Pools can detach from a Facility with `facilityId: null`.
- [x] Full PoolInput preservation reviewed and approved.
- [x] Facility selector rejects malformed/non-canonical Facility IDs.
- [x] Pool list, dashboard, Pool detail, and provider-portfolio cache invalidation handled as required.
- [x] Admin authorization preserved.
- [x] Provider Facility management remains out of scope.
- [x] Facility grants/inheritance remain unimplemented.
- [x] GPT-5.5 final recheck: FINDINGS NONE / READY TO COMMIT.
- [x] Project Wiki validator: valid=true, errors=0, warnings=0.
- [x] Canonical typechecks and build passed.
- [x] Integration suite remained non-blocking because no backend/API/DB/generated changes were made.
- [x] Commit pushed: `bec57bc Add pool facility assignment UI`.

## Latest Milestone Closure — P1 Delegated Maintenance & Backwash

- [x] Provider delegated Pool workspace now exposes maintenance history.
- [x] Authorized provider admin/technician can record maintenance when `canMaintain` permits.
- [x] Provider delegated Pool workspace now exposes filter-backwash history.
- [x] Authorized provider admin/technician can record backwash when `canBackwash` permits.
- [x] Existing delegated measurement workflow preserved.
- [x] Backend authorization/provenance remains authoritative.
- [x] No backend, OpenAPI, generated-client, DB, schema, or migration changes.
- [x] Delegated maintenance photo evidence intentionally disabled because current photo endpoints remain owner-scoped.
- [x] Provider planned-work execution intentionally disabled in shared backwash component for this slice.
- [x] Owner photo evidence and owner planned-work behavior preserved through default-compatible shared-component props.
- [x] Provider Facility management remains unresolved/deferred.
- [x] Facility grants/inheritance remain unresolved.
- [x] Later P1 work remains pending: corrective-action/verification, provider dosage, and cross-org planned work/provider-member assignment where justified.
- [x] GPT-5.5 final recheck: FINDINGS NONE / READY TO COMMIT.
- [x] Typecheck and PoolCheck build passed.
- [x] Integration skipped non-blockingly because TEST_DATABASE_URL was unavailable through the safe workflow and this slice made no backend/API/DB/generated changes.
- [x] Project Wiki validator: valid=true, errors=0, warnings=0.
- [x] Commit pushed: `04765c6 Add delegated maintenance and backwash UI`.

## Latest Milestone Closure — Provider Corrective Actions + Verification UI

- [x] Implemented frontend-only on delegated provider Pool detail.
- [x] corrective-action history displayed.
- [x] provider admin + canManageCorrectiveActions: mark pending corrective action applied, dismiss pending corrective action.
- [x] provider admin + canVerify: verify applied/unverified corrective actions.
- [x] non-admin users remain read-only even if capability flags exist.
- [x] backend remains final authorization authority.
- [x] Verification: normal recent measurement selector retained.
- [x] Recent measurements NOT treated as exhaustive (backend list is capped).
- [x] Manual fallback: "Usar otra medición por ID" with canonical positive safe integer validation.
- [x] Rejects whitespace, leading zero, sign, decimals, scientific notation, unsafe integers.
- [x] No arbitrary measurement fetch by ID.
- [x] Backend validates pool/org/access/timing/original measurement/required parameter.
- [x] Corrective parameter value shown in measurement options.
- [x] Parameter-missing measurements show "sin dato" and are disabled.
- [x] OUT_OF_RANGE_EFFECTIVE_CONFIRMATION_REQUIRED remains explicit two-step confirmation.
- [x] Relevant state changes clear stale confirmation.
- [x] Explicitly NOT added: provider corrective creation, recommendations, apply-product, dosage/inventory, canDose changes, backend/API/OpenAPI/generated/DB/schema changes, Facility changes, planned-work changes, owner redesign.
- [x] Security: no raw createdByUserId/resolvedByUserId/verifiedByUserId/grant/relationship IDs exposed.
- [x] GPT-5.5 final commit-gate: FINDINGS NONE / READY TO COMMIT.
- [x] pnpm run typecheck:poolcheck PASS.
- [x] pnpm run build:poolcheck PASS.
- [x] git diff --check PASS.
- [x] Prior full/typecheck validations in slice passed.
- [x] Integration not required for frontend-only change; existing delegated backend corrective/verification integration coverage already exists.
- [x] Commit pushed: `2fccccf Add delegated corrective action verification UI`.

## Next Quality Milestone

Planned, not started.

After this milestone, perform a separate full PoolCheck UI/UX audit.

Audit model:
- GPT-5.5
- READ ONLY first
- explicit skills:
  - obsidian
  - design-md
  - make-interfaces-feel-better

Audit by surface rather than one giant redesign:
- global shell/navigation
- dashboard/pools
- owner Pool detail
- Facilities
- Provider Portfolio
- Provider Pool Detail
- operational cards/forms/dialogs
- loading/empty/error states
- mobile/responsive
- global visual consistency

Rules:
- preserve existing PoolCheck operational design language
- no global redesign by assumption
- group systemic findings
- prioritize HIGH/MEDIUM/LOW
- DeepSeek implements resulting improvements in bounded slices
- GPT-5.5 reviews each slice

Also note that the same UI/UX audit methodology is intended for StockCheck separately.

## Next Product Roadmap

Do not automatically start a product feature.
After the UI/UX audit planning/decision, remaining P1 product candidates still include:
- cross-org planned work/provider-member assignment where justified

Provider Facility management and Facility grant inheritance remain unresolved/deferred and must not be started by assumption.

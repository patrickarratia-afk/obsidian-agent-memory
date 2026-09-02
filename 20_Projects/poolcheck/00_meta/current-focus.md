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

HEAD:

`04765c6 Add delegated maintenance and backwash UI`

Working tree was clean at the close of P1 7E-B.

## Recently Completed

- [x] Facility foundation — Organization → Facility → Pool
- [x] Facility CRUD API and Pool assignment contract
- [x] Facility-aware Pool filtering
- [x] Provider Facility portfolio enrichment/filter
- [x] Provider operational-status enrichment/filter
- [x] Canonical Project Wiki 1.4.0 installed and validated (0 errors / 0 warnings)

P1 portfolio filtering dimensions now covered:

- client / organization
- Facility
- Pool/search
- operational status

## Current Objective

Paused after successful closure of P1 Delegated Maintenance & Backwash Provider UI.

The next known P1 roadmap candidate is corrective-action / verification workflow UI, followed later by provider dosage and cross-organization planned work / provider-member assignment where justified.

Before implementation, confirm the next canonical slice from the current Project Wiki, repository state, authorization model, and tests.

Do not start provider Facility management or Facility grants/inheritance by assumption; both remain unresolved/deferred.

## Explicitly Deferred

Do not fold these into 7E-B:

- Pool → Facility assignment UI
- provider Facility management
- Facility hierarchy redesign
- Facility grants/inheritance
- location → Facility conversion/backfill
- DB schema/migrations
- provider status N+1 optimization
- unrelated redesign

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

## Next Session

Before implementing 7E-B:

1. read `VAULT_RULES`
2. read `_project`
3. read this `current-focus`
4. confirm Git branch/status/HEAD
5. inspect exact auth, route, navigation, CRUD and generated Facility-hook patterns
6. use Serena when useful
7. use Graphify only if architectural dependency information is genuinely needed

Current preferred implementation model while native Codex quota is unavailable:

DeepSeek V4 Flash through Hermes/OpenRouter.

A GPT-5.5 review should be used for sensitive authorization/permission changes when quota is available.

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

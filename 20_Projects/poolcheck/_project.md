---
type: project
scope: project
project: poolcheck
area: software-engineering
status: active
source_date: 2026-09-02
reviewed: true
owner: patrick
aliases: [PoolCheck, poolcheck-app]
tags: [project, poolcheck]
---

# Project: PoolCheck

## Canonical Repo

`/home/patrick/Apps/PoolCheck`

Application workspace:

`/home/patrick/Apps/PoolCheck/Pool-Monitor-Pro`

## Purpose

Lightweight operational-memory layer for PoolCheck development sessions. This vault stores only the minimum continuation context needed to resume work efficiently.

It must not become a duplicate of the Project Wiki or the repository.

## Product Vision

PoolCheck is a provider-independent platform for operating and technically supervising aquatic facilities.

Core structure:

Organization → Facility → Pool

The facility/client organization owns its pools and may have its own operators.

External service providers may supervise multiple client organizations through delegated access and one provider identity.

Teslaquim may be a pilot provider, but PoolCheck must remain structurally independent from Teslaquim and capable of supporting other providers.

## Authority Hierarchy

| Priority | Source | Role |
|----------|--------|------|
| 1 | Current repo code, Git history, migrations, passing tests | Ultimate source of truth |
| 2 | `.project-wiki/` at canonical repo path | Durable decisions, requirements, architecture, project state |
| 3 | This Obsidian vault | Compact operational context and session continuity |

Resolution rules:

- Obsidian vs Project Wiki → prefer Project Wiki unless current repo/tests disprove it
- Either memory layer vs repo/tests → trust repo/tests
- Graphify and Serena are supporting tools, not canonical state

## Operational Tool Roles

- ChatGPT: architecture, continuity, supervision, decisions
- GPT-5.5: architecture, auth/isolation, sensitive reviews, final critical review
- DeepSeek V4 Flash: routine implementation and well-bounded multi-file work
- Hermes: primary agent launcher/orchestrator
- Obsidian: operational memory
- Serena: symbols, references, structural code navigation
- Graphify: optional architecture/dependency analysis
- Git/tests/diff/status: final technical authority

## Default Model-Routing Workflow

GPT-5.5:
- architecture
- planning
- security-sensitive inspection
- auth/roles/capabilities
- org/provider/facility isolation
- API/data-model decisions
- final review / commit-gate

DeepSeek V4 Flash:
- primary implementation workhorse
- bounded frontend implementation
- routine multi-file changes
- tests
- mechanical refactors
- fixes from GPT reviews
- documentation updates with clear acceptance criteria

Default cycle:
GPT-5.5 plans/reviews → DeepSeek implements → GPT-5.5 commit-gate → fixes if needed → commit/push

Important:
- Only one writing agent may modify a given working tree at a time.
- Parallel read-only sessions are allowed.
- Parallel implementation requires separate git worktrees/branches.

## PoolCheck Skill Routing

Enabled does NOT mean actually used.

For important Hermes tasks:
- prompts must explicitly specify relevant skills to load/use
- agents must report at the end:
  - skills actually loaded/used
  - why
  - relevant enabled skills deliberately not used
  - why not

PoolCheck skill routing:
- obsidian: operational memory/continuity
- security-and-hardening: auth, roles, capabilities, isolation, trust boundaries, sensitive inputs
- api-and-interface-design: contracts, generated clients, API/module boundaries
- design-md: hierarchy, layout, responsive operational UX
- make-interfaces-feel-better: restrained UI polish
- performance-optimization: only with actual performance evidence
- defuddle: only for external web/document extraction

Do not load every installed skill by default.

## Environment Protection

Production and real customer data are off-limits unless explicitly approved by the human operator.

Agents must not:

- inspect or expose production DATABASE_URL or secrets
- use real customer data as test data
- run destructive cleanup
- mix organizations/tenants
- weaken Facility ownership boundaries
- weaken provider portfolio/grant boundaries

DEV/local/test environments may be used according to repository rules.

## Path to Durable Knowledge

Start with:

`20_Projects/poolcheck/00_meta/`

Then:

`.project-wiki/INDEX.md`

Escalate to repo/tests, Serena, and optionally Graphify only as needed.

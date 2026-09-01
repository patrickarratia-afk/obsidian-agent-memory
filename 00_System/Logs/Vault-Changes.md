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

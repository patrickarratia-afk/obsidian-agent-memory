---
type: context-capsule
scope: project
project: example-app
status: active
source_date: 2026-04-19
reviewed: false
tags: [context-capsule, build-test]
---

# Capsule: Build & Test — example-app

## Purpose

Retrieve this before running any build, test, lint, or verification command.

## Key boundaries

| Command | What it does |
|---------|-------------|
| `npm run dev` | Start dev server (port 3000) |
| `npm run build` | Production build |
| `npm test` | Run Vitest unit tests |
| `npm run lint` | Lint all source files |

## Common failure modes

- Running `npm run build` while the dev server is active can corrupt the `.next/` directory.
- `npm test` only runs unit tests — E2E tests require a separate `npx playwright test` invocation.

## What not to assume

- `npm run lint` may not lint all config files — check the lint config if a config file error slips through.

## Evidence basis

Compressed from: `repo-map.md` § Key Scripts, `architecture-index.md` § Failure Surfaces.
**Staleness:** Review after 45 days per STALENESS_POLICY (volatile domain).

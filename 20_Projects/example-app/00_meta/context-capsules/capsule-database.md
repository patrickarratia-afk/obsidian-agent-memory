---
type: context-capsule
scope: project
project: example-app
status: active
source_date: 2026-04-19
reviewed: false
tags: [context-capsule, database]
---

# Capsule: Database — example-app

## Purpose

Retrieve this before adding columns, writing migrations, or debugging database errors.

## Key boundaries

| Domain | Boundary Fact |
|--------|--------------|
| ORM | Prisma / SQLite |
| Schema location | `prisma/schema.prisma` |
| Migration command | `pnpx prisma migrate dev --name <description>` |
| Seeding | `pnpx prisma db seed` |

**Generated code:** Prisma client lives in `node_modules/.prisma/client`. Do not edit manually.

## Common failure modes

- Writing a raw SQL fetch without checking `schema.prisma`.
- Running the UI server without running `pnpx prisma generate` after a pull.

## Evidence basis

Compressed from: `repo-map.md`, `architecture-index.md` § Persistence.
**Staleness:** Review after 90 days per STALENESS_POLICY (stable domain).

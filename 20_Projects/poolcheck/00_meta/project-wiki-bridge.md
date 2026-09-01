---
type: reference
scope: project
project: poolcheck
status: active
reviewed: true
tags: [bridge, reference]
---

# Project Wiki Bridge — PoolCheck

## Role of Project Wiki

The PoolCheck `.project-wiki/` at the canonical repository root is the durable knowledge layer for architecture, requirements, decisions, API/data-model documentation, security rules, roadmap, risks, and durable business rules.

Canonical repository:

`/home/patrick/Apps/PoolCheck`

Project Wiki entrypoint:

`/home/patrick/Apps/PoolCheck/.project-wiki/INDEX.md`

Schema:

`project-wiki 1.4.0`

The initial Project Wiki scan was structurally validated on 2026-09-01 with the canonical `project-wiki` validator:

- valid: true
- errors: 0
- warnings: 0

## Role of Obsidian Agent Memory

This vault is the compact operational continuation layer.

It stores only the minimum context required to resume PoolCheck work efficiently and must not duplicate Project Wiki content.

## Retrieval Hierarchy

1. `00_System/AI/VAULT_RULES.md`
2. `20_Projects/poolcheck/_project.md`
3. `20_Projects/poolcheck/00_meta/current-focus.md`
4. relevant context capsule only when justified
5. `.project-wiki/INDEX.md`, then one specific linked Wiki page
6. current repo / Git / migrations / tests
7. Serena for symbols and references
8. Graphify only when architecture/dependency evidence is genuinely useful

Stop retrieval once enough trustworthy context exists.

## Authority

If Obsidian conflicts with Project Wiki, prefer the Project Wiki unless current repository evidence disproves it.

If either memory layer conflicts with current code, Git history, migrations, or passing tests, trust the repository and tests.

## Tool Roles

| Tool | When to use |
|------|-------------|
| Project Wiki | Durable architecture, decisions, requirements, security, roadmap |
| Obsidian | Session continuation and operational focus |
| Serena | Symbols, references, declarations, structural navigation |
| Graphify | Optional architecture/dependency analysis |
| Git/tests | Final technical authority |

## Environment Safety

PoolCheck must remain structurally independent from Teslaquim.

Do not access production or real customer data without explicit human approval.

Preserve:

- organization isolation
- provider portfolio boundaries
- roles and permissions
- Facility ownership
- delegated provider access
- auditability

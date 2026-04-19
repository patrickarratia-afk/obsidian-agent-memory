---
type: system
scope: global
status: active
reviewed: true
tags: [system, rules]
---

# Vault Rules

All AI tools and humans must read this file before acting on this vault.

## Decision Hierarchy

1. Raw sources are immutable evidence — never edit files in any `raw/` folder.
2. Human-reviewed decision notes outrank AI summaries.
3. Wiki pages are derived artifacts and must cite their source notes.
4. Global knowledge is promoted from project wikis to `10_Global/wiki/` only after human review.
5. Do not create parallel systems — check existing folders, templates, and note types before adding anything new.

## Folder Map

| Folder | Purpose |
|--------|---------|
| `00_System/AI/` | Vault rules and AI tool config |
| `00_System/Templates/` | Note templates |
| `00_System/Dashboards/` | Obsidian Bases dashboard files |
| `00_System/Logs/` | Vault change log |
| `01_Inbox/Fleeting/` | Quick fleeting notes |
| `01_Inbox/Capture/` | Clippings, pastes, raw captures |
| `01_Inbox/Unprocessed/` | Items awaiting triage |
| `02_Daily/` | Daily notes, one per day |
| `10_Global/raw/` | Immutable source files and clippings |
| `10_Global/wiki/entities/` | Named entities (people, orgs, products) |
| `10_Global/wiki/concepts/` | Abstract concepts and definitions |
| `10_Global/wiki/topics/` | Subject-area overviews |
| `10_Global/wiki/patterns/` | Reusable patterns and heuristics |
| `10_Global/wiki/source-digests/` | AI-compiled digests of source material |
| `20_Projects/` | Active project folders |
| `20_Projects/_Registry/` | Project index and status tracking |
| `20_Projects/_Template/` | Reusable project folder template |
| `30_Areas/` | Ongoing responsibilities and domains |
| `40_Assets/images/` | Image files |
| `40_Assets/pdfs/` | PDF documents |
| `40_Assets/audio/` | Audio files |
| `40_Assets/web/` | Saved web content |
| `40_Assets/canvas/` | Obsidian canvas files |
| `99_Archive/` | Completed or inactive material |

## Naming Rules

- Dated notes: `YYYY-MM-DD_title.md`
- Reference notes: `Title.md` (title-case)
- Top-level folders: numbered prefix (`00_`, `10_`, etc.)
- Meta folders: underscore prefix (`_Registry`, `_Template`)

## Portability

- Plain markdown only. No plugin-specific syntax outside `.obsidian/`.
- Frontmatter properties use the standard schema defined in `00_System/Templates/`.
- `.base` files are Obsidian Bases dashboards — they degrade gracefully outside Obsidian.
- Every note must be readable and useful outside Obsidian.

## Property Schema (all templates)

```
type, scope, project, area, status, source_url, source_title,
source_date, reviewed, owner, aliases, tags
```

## Operating Model

| Layer | Zone | Rule |
|-------|------|------|
| Raw | `raw/` folders (any level) | Immutable evidence — never edit |
| Wiki | `10_Global/wiki/` | AI-compiled, human-reviewed |
| Decisions | project `decisions/` folders | Explicit human records, `reviewed: true` required |
| Projects | `20_Projects/` | Scoped knowledge, promote to global only after review |

## Project Folder Structure

Every project under `20_Projects/` follows `_Template/`:

```
project-name/
├── 00_meta/      ← project metadata notes
├── raw/          ← immutable sources (do not edit)
├── wiki/         ← project-scoped knowledge
├── work/         ← active work notes
├── meetings/     ← meeting notes
├── decisions/    ← decision records
├── specs/        ← specifications and designs
├── outputs/      ← deliverables and artifacts
├── archive/      ← completed sub-tasks
└── _project.md   ← project index note
```

## AI Tool Constraints

- Do not modify `.obsidian/` unless explicitly asked.
- Treat any `raw/` subfolder as immutable — read only.
- Create only `.md` and `.base` files.
- Follow the property schema defined in the templates.
- Check existing notes before creating new ones to avoid duplication.
- Log significant vault changes in `00_System/Logs/Vault-Changes.md`.

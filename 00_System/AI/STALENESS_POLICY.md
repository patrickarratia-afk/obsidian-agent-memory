---
type: system
scope: global
status: active
reviewed: true
tags: [system, protocol]
---

# Staleness Policy

Rules for identifying, reviewing, and handling notes that may be out of date.

## Staleness Thresholds

| Note Type | Review After | Action if Stale |
|-----------|-------------|-----------------|
| `current-focus.md` | 2 weeks without update | Rewrite or mark `status: stale` |
| `repo-map.md` | 60 days | Re-map from repo or mark `status: stale` |
| `architecture-index.md` | 90 days or after major refactor | Review and update |
| `authority-map.md` | 90 days or after team change | Review and update |
| `glossary.md` | 180 days | Spot-check for obsolete terms |
| Context capsule (volatile: build-test, deployment, auth, ai-integrations) | 45 days | Re-verify key boundaries from repo or mark `status: stale` |
| Context capsule (stable: database, domain-model, sync, architecture) | 90 days | Spot-check key boundaries against repo state |
| Project `wiki/` notes | 90 days | Review; promote, archive, or update |
| Global `wiki/` notes | 180 days | Review; update or archive |
| Decision records | Never expire | Add a superseded link if overridden |
| Raw source files | Never expire | Immutable — do not review or edit |
| Daily notes | Never expire | Archive after 90 days |

## Stale Status Workflow

1. Mark the note: `status: stale` in frontmatter.
2. Add a comment at the top of the note body:
   ```
   > **Stale** — last verified YYYY-MM-DD. Needs review.
   ```
3. Move to `archive/` only when the note is fully superseded and no longer useful as reference.

## Do Not Delete

Prefer archiving over deleting. Deleted notes lose history. Move to the nearest `archive/` folder.

## AI Tool Responsibility

When an AI tool reads a note with `status: stale` or `reviewed: false`, it must:
- Treat the content as unverified.
- Not propagate unverified facts to other notes without flagging them.
- Suggest a review if it has observed conflicting or updated information.

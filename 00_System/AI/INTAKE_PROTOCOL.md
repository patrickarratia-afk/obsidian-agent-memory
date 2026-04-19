---
type: system
scope: global
status: active
reviewed: true
tags: [system, protocol]
---

# Intake Protocol

Rules for capturing new information from external repos and sources into this vault.

## Triage Tiers

| Tier | What | Where |
|------|------|-------|
| 1 — Fleeting | Rough notes, unverified observations | `01_Inbox/Fleeting/` |
| 2 — Capture | Clippings, pastes, raw output from tools | `01_Inbox/Capture/` |
| 3 — Unprocessed | Items needing triage but too long to read now | `01_Inbox/Unprocessed/` |

## Intake Rules

1. **Raw evidence goes to `raw/` folders — never summarize in place.**
   Copy verbatim output (logs, file listings, API responses) into a project's `raw/` folder using T_Source. Do not edit it after saving.

2. **Use T_Source for any external document or output.**
   Fill `source_url`, `source_title`, and `source_date`. If unknown, write `UNKNOWN`.

3. **AI-generated summaries are not evidence.**
   Label AI-compiled notes with `reviewed: false` until a human has checked them.
   Never place an unreviewed AI summary directly into `wiki/`.

4. **One file per source.**
   Do not merge multiple sources into one raw file. Keep them atomic.

5. **Date all intake notes.**
   Use `source_date` for when the source was created/retrieved. Use `YYYY-MM-DD`.

6. **Mark fabrications as UNKNOWN.**
   If a detail is not confirmed from a source, write `UNKNOWN`. Do not infer.

## Processing Flow

```
Capture → 01_Inbox/ → triage → project raw/ or wiki/ → promote to 10_Global/wiki/ after review
```

## When to Bypass Inbox

You may write directly to a project folder (skipping Inbox) when:
- The source is already identified and the target project is known.
- You are updating a named stub (e.g. `repo-map.md`) from direct observation.

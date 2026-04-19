---
type: system
scope: global
status: active
reviewed: true
tags: [system, protocol]
---

# Promotion Rules

Rules for when and how project-scoped knowledge moves to the global wiki.

## What Can Be Promoted

A note is eligible for promotion to `10_Global/wiki/` when:

1. It captures a concept, pattern, or entity that applies to **more than one project**.
2. It has been **reviewed by a human** — `reviewed: true` in frontmatter.
3. It is **not project-specific** — it contains no details that only make sense in one project's context.
4. It is **durable** — unlikely to become stale within 6 months without a major change.

## What Must Not Be Promoted

- Raw source files (`raw/` contents stay in place — they are evidence, not knowledge).
- Unreviewed AI summaries.
- Notes marked `status: stub` — stubs must be populated first.
- Meeting notes, work-in-progress drafts, or decision records (decisions stay in the project `decisions/` folder as a historical record).

## Promotion Procedure

1. Review the note. Set `reviewed: true` and `scope: global`.
2. Remove project-specific frontmatter (`project:` field, if applicable).
3. Move or copy the note to the correct subfolder of `10_Global/wiki/`:
   - Named entities → `entities/`
   - Abstract concepts → `concepts/`
   - Subject overviews → `topics/`
   - Reusable patterns → `patterns/`
   - Source summaries → `source-digests/`
4. Add a row to [[10_Global/wiki/log]] recording: date, note title, source project, reviewer.
5. If the original note remains in the project wiki, add a link: `→ Promoted to [[10_Global/wiki/...]]`.

## Promotion Is Not Deletion

Keep the project-scoped version if it contains project-specific context. The global version should be the distilled, general-purpose form.

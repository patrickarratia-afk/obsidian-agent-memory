---
type: system
scope: global
status: active
reviewed: true
tags: [system, protocol]
---

# Session Closeout Protocol

What to do — and what NOT to do — when a coding session ends. Designed for AI tools and humans alike.

**Default: leave Obsidian vault unchanged.** Update only when a clear trigger below is met.

---

## Update Triggers

### Update Obsidian only when operational continuation context materially changes

| What changed in repo | What to update in vault |
|---------------------|------------------------|
| Current focus / next concrete task changed | `current-focus.md` — update, do not mark partial progress |
| Feature or milestone completed | `current-focus.md` — mark complete, set next focus |
| Important blocker appeared or disappeared | `current-focus.md` — note the blocker |
| A durable boundary changed and a capsule would otherwise become incorrect | Relevant context capsule — update facts only |
| Staleness threshold exceeded per STALENESS_POLICY | Relevant capsule — re-verify and update `source_date` |

### Do NOT update Obsidian merely because

- Styling changed
- A small bug was fixed
- Formatting or whitespace changes
- Mechanical refactoring happened
- Project Wiki was updated but operational context did not change

### Add a decision note (`decisions/`) when

- A non-obvious architectural choice was made (e.g., chose library A over B, rejected a pattern).
- A constraint was formally established (e.g., "we will not use X because Y").
- A previous decision was superseded — add a `superseded by:` link, do not delete the old record.

Do **not** write a decision note for implementation details — those belong in code comments.

### Revise a context capsule when

- A FACT in the capsule is now incorrect (verified from repo).
- A new high-value boundary was established (passes the 3-evidence gate).
- The capsule's staleness threshold has passed — re-verify facts and update `source_date`.

Do **not** revise a capsule to add inferences or speculation. FACT-only.

### Append `Vault-Changes.md` when

- A new file or folder was created in the vault.
- A system protocol was modified.
- A project's `00_meta/` structure changed.

Do **not** append Vault-Changes.md for routine note edits (updating current-focus, adding a decision).

---

## When to Leave the Vault Unchanged

Leave the vault alone when:

- The session was read-only (you consulted vault notes but made no repo changes).
- The repo change was minor (typo fix, comment update, whitespace) — no vault-worthy facts changed.
- You are uncertain about a fact — do not record uncertain information. Mark it `UNKNOWN` if you must write it.
- A capsule or note already accurately reflects the current state — do not re-write correct content.

---

## Vault Health Spot-Check

Run this after any session that made structural changes to the vault:

1. **Stale status**: Scan the active project's `00_meta/` for notes with `status: stale`. Are they still needed?
2. **Capsule drift**: For any capsule you read this session — do its FACT entries still match repo reality?
3. **Unreviewed propagation**: Check that no `reviewed: false` note was used as authoritative input to another note without flagging it.
4. **Broken intent**: If `current-focus.md` still lists a task that was completed more than 2 sessions ago, update it now.

This check should take under 5 minutes. If it requires more time, the vault has drifted — re-read RETRIEVAL_PROTOCOL and prioritize the highest-staleness items.

---

## Sequence

```
Task complete → check update triggers → apply only what triggered → health spot-check → done
```

Resist the urge to "tidy up" notes that weren't touched by the session. Unsolicited edits introduce drift.

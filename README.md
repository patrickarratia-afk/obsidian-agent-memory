# Obsidian Agent Memory

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Works with: Claude](https://img.shields.io/badge/Works_with-Claude-orange)](CLAUDE.md)
[![Works with: Gemini](https://img.shields.io/badge/Works_with-Gemini-blue)](GEMINI.md)
[![Works with: Cursor](https://img.shields.io/badge/Works_with-Cursor-purple)]()
[![Works with: Copilot](https://img.shields.io/badge/Works_with-Copilot-cyan)]()
[![Works with: Windsurf](https://img.shields.io/badge/Works_with-Windsurf-teal)]()

**A production-grade memory system for AI coding agents.**

Stop dealing with agents that forget previous architectural decisions, hallucinate repo states, or burn tokens reading your entire codebase just to fix a typo.

> Clone → Open in Obsidian → Point your AI agent → Start coding with memory.

---

## The Problem

Karpathy's [LLM Wiki pattern](https://x.com/karpathy/status/1880365337488875564) and projects like [`obsidian-wiki`](https://github.com/Ar9av/obsidian-wiki), [`second-brain`](https://github.com/NicholasSpisak/second-brain), and [`llm-wiki-compiler`](https://github.com/ussumant/llm-wiki-compiler) are excellent for general knowledge management. But they're designed for knowledge ingestion — not for the tight feedback loop of active software development, where:

1. **Token budgets matter** — agents read everything, even when they only need one fact.
2. **Vaults bloat** — agents over-update notes, introducing drift and noise.
3. **Repo truth gets ignored** — a vault note says 416 tests, but the repo now has 500. The agent trusts the vault and hallucinates.

## The Solution

**Obsidian Agent Memory** introduces three patterns that fix this:

### 🧊 Context Capsules
Dense, 60-line-max notes that compress operational knowledge into retrievable boundaries. Instead of reading a 300-line architecture doc, your agent reads `capsule-database.md` and knows exactly what ORM you use, where the schema lives, and what breaks if you touch it.

### 📶 Tiered Retrieval Protocol
A cost-conscious reading order: capsules first, full docs only if needed. Most coding tasks resolve at Tier 2 — agents stop escalating as soon as they have the answer.

```
Tier 0: VAULT_RULES.md (always)
Tier 1: _project.md + current-focus.md
Tier 2: Context capsule for the task domain  ← stop here for most tasks
Tier 3: Full 00_meta/ notes (repo-map, architecture-index)
Tier 4: Project wiki/ pages
Tier 5: raw/ sources (last resort)
```

### ⚖️ Contradiction Resolution
**Repo truth always overrides vault summaries.** If an agent observes a conflict, it must flag it, trust the repo, and update the vault note. No silent hallucination.

---

## What's Inside

```
obsidian-agent-memory/
├── AGENTS.md                          ← agent entrypoint (generic)
├── CLAUDE.md                          ← Claude Code entrypoint
├── GEMINI.md                          ← Gemini CLI entrypoint
├── Home.md                            ← vault home page
│
├── 00_System/
│   ├── AI/
│   │   ├── VAULT_RULES.md             ← master rules (read first)
│   │   ├── RETRIEVAL_PROTOCOL.md      ← tiered retrieval order
│   │   ├── SESSION_CLOSEOUT_PROTOCOL.md ← when to update / leave alone
│   │   ├── STALENESS_POLICY.md        ← freshness thresholds
│   │   ├── INTAKE_PROTOCOL.md         ← how to capture new info
│   │   └── PROMOTION_RULES.md         ← when project→global promotion
│   ├── Templates/                     ← note templates (6 types)
│   └── Logs/Vault-Changes.md         ← structural change log
│
├── 20_Projects/
│   ├── _Template/                     ← copy this for new projects
│   │   └── 00_meta/context-capsules/README.md  ← capsule creation rules
│   └── example-app/                   ← working example project
│       └── 00_meta/
│           ├── _project.md
│           ├── current-focus.md
│           └── context-capsules/
│               ├── capsule-database.md
│               └── capsule-build-test.md
│
├── 01_Inbox/                          ← captures, fleeting notes
├── 10_Global/wiki/                    ← cross-project knowledge
├── 30_Areas/                          ← ongoing responsibilities
└── 99_Archive/                        ← completed material
```

**Two files to start:** Only `VAULT_RULES.md` and `RETRIEVAL_PROTOCOL.md` are required reading. Everything else is reference.

---

## Quick Start

```bash
git clone https://github.com/mithunyc/obsidian-agent-memory.git
```

1. Open the cloned folder as a **Vault** in [Obsidian](https://obsidian.md).
2. Open `Home.md` — this is your dashboard.
3. Explore `20_Projects/example-app/` to see context capsules in action.
4. Copy `20_Projects/_Template/` and rename it for your own project.
5. Tell your AI agent:

> "My memory system is at `[path-to-vault]`. Start by reading `00_System/AI/VAULT_RULES.md` and `00_System/AI/RETRIEVAL_PROTOCOL.md`."

Or just point it at `AGENTS.md` / `CLAUDE.md` / `GEMINI.md` in the vault root — it handles the rest.

---

## The Workflow

```
Start session → Agent reads capsules (Tier 0–2) → Execute task → Session closeout → Done
```

1. **Start:** Agent reads `_project.md`, `current-focus.md`, and the relevant capsule.
2. **Code:** Agent works with full operational context.
3. **Close:** Agent runs `SESSION_CLOSEOUT_PROTOCOL.md` — updates only what changed, leaves everything else alone.

---

## Works With

| Agent | Config File | Status |
|-------|------------|--------|
| Claude Code | `CLAUDE.md` | ✅ Tested |
| Gemini CLI / Antigravity | `GEMINI.md` | ✅ Tested |
| Cursor | `AGENTS.md` | ✅ Compatible |
| GitHub Copilot | `AGENTS.md` | ✅ Compatible |
| Windsurf | `AGENTS.md` | ✅ Compatible |
| Any agent that reads markdown | `AGENTS.md` | ✅ Compatible |

---

## Inspired By

- Andrej Karpathy's [LLM Wiki pattern](https://x.com/karpathy/status/1880365337488875564)
- [`obsidian-wiki`](https://github.com/Ar9av/obsidian-wiki) — tiered retrieval influence
- [`second-brain`](https://github.com/NicholasSpisak/second-brain) — three-layer architecture
- [`llm-wiki-compiler`](https://github.com/ussumant/llm-wiki-compiler) — coverage indicators concept
- [`wiki-skills`](https://github.com/kfchou/wiki-skills) — wiki-lint health checks

What this project adds: **Context Capsules**, **Contradiction Resolution**, **Session Closeout with leave-alone rules**, and a **Tiered Retrieval Budget** specifically designed for the tight loop of active software development.

---

## Contributing

Contributions welcome. If you've built capsule patterns for new domains (auth, deployment, CI/CD, monitoring), open a PR to add them as examples.

## License

[MIT](LICENSE) — free to use, fork, and extend.

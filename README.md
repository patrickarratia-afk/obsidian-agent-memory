# Obsidian Agent Memory

A production-grade memory system for AI coding agents (Claude, Gemini, Cursor, Copilot). 

Stop dealing with agents that forget previous architectural decisions, hallucinate repo states, or spend hundreds of thousands of tokens reading your entire codebase just to fix a typo.

This is NOT an automated ingest tool. This is a disciplined, human-in-the-loop operational vault. It focuses on the **Context Capsule Pattern** — dense, fact-based boundaries that tell an agent exactly how to act within a specific codebase domain.

## Why this exists

Karpathy's LLM Wiki pattern and derivative projects (`obsidian-wiki`, `second-brain`, `llm-wiki-compiler`) are fantastic for general knowledge management. But they fail for active software development because:
1. They lack a cost-conscious retrieval protocol.
2. They over-update, creating "vault bloat".
3. They don't enforce a "repo truth overrides vault summaries" rule.

**Obsidian Agent Memory** fixes this. 

## Features

- **Tiered Retrieval Protocol**: Agents are instructed to read capsules first, and stop escalating if they have their answer. Major API token savings.
- **Context Capsules**: 60-line max notes that compress operational knowledge (e.g. `capsule-database.md`, `capsule-build-test.md`).
- **Contradiction Resolution Engine**: A strict rule that the repo state always overrides the vault state, forcing agents to correct the vault rather than hallucinate.
- **Session Closeout Checklists**: Explicit "leave it alone" rules so agents only update the vault when facts change, preventing note drift.
- **Vendor-Agnostic**: Works out of the box with `claude`, `gemini-cli`, `cursor` agents, or any other tool that can read arbitrary markdown paths.

## Quick Start
1. Clone this repository to a local folder: `git clone https://github.com/YOUR_GITHUB_HANDLE/obsidian-agent-memory.git`
2. Open the folder as a Vault in Obsidian.
3. Open `Home.md`. 
4. Check out `20_Projects/example-app` to see how a Context Capsule is written.
5. In your AI Agent, point it to the vault: "My memory system is located at `[path-to-vault]`. Start by reading `00_System/AI/VAULT_RULES.md` and `00_System/AI/RETRIEVAL_PROTOCOL.md`."

## The Workflow
1. When you start an AI coding session, point the agent to the project's meta notes via the tiered retrieval protocol.
2. The agent executes the task using the known boundaries.
3. When the session ends, the agent runs the `SESSION_CLOSEOUT_PROTOCOL.md` to spot-check for stale notes, update any mutated facts in the context capsules, and record completed tasks.

## License
MIT License. Free to use, bend, and break. Designed to prevent reinventing the wheel for agentic workflows.

# AGENTS

Reusable **agent instruction file** (orchestrator prompt) for AI coding assistants. This is a drop-in `AGENTS.md`-style system instruction — not application code. Copy it into a project's root and let the agent adapt it during the mandatory first-session setup.

## Contents

| File | Target agent | Notes |
| ---- | ------------ | ----- |
| `AGENTS_with_brain.md` | Agent-agnostic template | Self-adapting variant: on first contact the agent researches the repo, asks for mission and goals, creates a `brain/` directory of project context, and rewrites the placeholders itself. Uses MCP tools where configured (`athenaeum`, `jcodemunch`). |

## Operating model

- **Self-setup on first contact** — a mandatory initial setup procedure: repo research via subagent, user interview for mission and goals, creation of the project brain, and in-place adaptation of every `[PLACEHOLDER]` and `<!-- setup: -->` comment.
- **Project brain** — `brain/BRAIN.md` is the front door to session-spanning context: mission, goals, decisions with rationale, and a `roadmap.md` Kanban board (`Backlog` / `In Progress` / `Testing` / `Done` / `Idea Bank`) that only the user may move cards to `Done` on.
- **Delegate by default** — the main session plans, decides, and reviews; exploration, research, bulk edits, and verification go to subagents with standalone prompts and compressed, evidence-backed reports.
- **MCP integrations:**
  - **Athenaeum** — durable knowledge library for lessons and decisions that outlive the repo; recalled at session start, written only by the main session; the brain is the local fallback.
  - **jCodeMunch** — symbol-level code retrieval via tree-sitter indexing to cut token usage; native read/grep/glob only as fallback and immediately before edits.
- **Language discipline** — no emojis anywhere; code, comments, and commit messages always in English.
- **Docs discipline** — every meaningful change requires a docs pass; each rule lives in exactly one owning doc; stale notes are deleted, not explained.
- **Release & Git conventions** — Semantic Versioning, a release checklist (version carrier, tag, release notes, verification), Conventional Commits, and no commits unless the user asks.

## Usage

1. Copy `AGENTS_with_brain.md` into the target project as `AGENTS.md` (or the agent's equivalent instructions file).
2. Start a session with the kick-off prompt embedded in the file's setup section — the agent runs the initial setup and adapts the file to the repo.
3. Ensure the referenced MCP servers (`athenaeum`, `jcodemunch`) are configured, or let setup remove those sections.

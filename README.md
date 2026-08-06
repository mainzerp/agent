# AGENTS

Reusable **agent instruction files** (orchestrator prompts) for AI coding assistants. These are drop-in `AGENTS.md`-style system instructions — not application code. Copy the variant matching your coding agent into a project's root and adapt the `PROJECT-NAME` placeholder.

## Contents

| File | Target agent | Notes |
| ---- | ------------ | ----- |
| `AGENTS_kimi-code.md` | [Kimi Code](https://github.com/MoonshotAI/kimi-cli) (CLI) | Uses the `Agent` / `AgentSwarm` tools and `AskUserQuestion` for clarification; subagents run as `subagent_type="coder"`; MCP tools are prefixed (`mcp__athenaeum__*`, `mcp__jcodemunch__*`). |
| `AGENTS_kilo-code.md` | [Kilo Code](https://github.com/Kilo-Org/kilocode) | Same instruction set, adapted to Kilo's `task` tool with `subagent_type="general"`, the `question` tool, and unprefixed MCP tool names. |

Both variants define the **same operating model**, differing only in tool names and agent vocabulary:

- **Orchestrator identity** — the agent you chat with is the single point of contact; it delegates research, planning, and implementation to subagents and supervises their work.
- **Mandatory workflow** — clarification → research (subagents write `docs/SubAgent/[NAME]/*_ANALYSIS.md`) → planning (`PLAN.md`) → explicit in-chat plan approval → implementation → final user confirmation. No implementation before plan approval.
- **Parallel execution** — up to 3 parallel subagents per phase for research and implementation, coordinated via a shared `CHANGES.md` protocol and a Merge & Verify pass.
- **MCP integrations:**
  - **Athenaeum** — durable knowledge library for lessons, decisions, and project context (queried at session start, updated at session end); `docs/project/lessons.md` is the local fallback.
  - **jCodeMunch** — symbol-level code retrieval via tree-sitter indexing to cut token usage; native read/grep/glob only as fallback.
- **Docs discipline** — every meaningful change requires a docs pass; rules live in exactly one owning doc; stale notes are deleted, not explained.
- **Release & Git conventions** — Semantic Versioning, a release checklist (`VERSION.md`, `__version__`, `pyproject.toml`, tag, GitHub release), and Conventional Commits.

## Usage

1. Pick the file matching your coding agent.
2. Copy it into the target project as `AGENTS.md` (or the agent's equivalent instructions file).
3. Replace `**PROJECT-NAME**` with the actual project name.
4. Ensure the referenced MCP servers (`athenaeum`, `jcodemunch`) are configured, or remove those sections if unused.

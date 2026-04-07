# .ai: Agentic Intelligence & Context Directory

This directory is the "Source of Truth" for AI agents (like Antigravity, Cursor, and Claude) interacting with this codebase.

## Directory Structure

- **`/docs/`**: Long-term architectural context, roadmap, and steering principles.
  - **`/docs/specs/`**: Functional requirements and technical specifications.
- **`glossary.md`**: Project-specific terminology to prevent semantic drift.
- **`.antigravity.json`**: Configuration for the Antigravity agent.
- **`.cursorrules`**: Context-specific rules for the Cursor IDE.
- **`AGENTS.md`**: Operations, workflows (Human-in-the-loop), and style guides for all AI agents.

## Why this exists?

In modern software development (2026+), managing **Agentic Context** is as critical as managing source code. By keeping these files structured in `.ai/`, we ensure that:
1. **Consistency**: All AI tools use the same rules and definitions.
2. **Persistence**: Decisions and constraints are documented for future agents.
3. **Efficiency**: Agents don't have to guess or rediscover the architect's intent.

---

> [!TIP]
> When starting a new task, tell your agent to "Read the .ai manifest" to ensure it has the latest context.

# .ai: Agentic Intelligence & Context Directory

This directory is the "Source of Truth" for AI agents (like Antigravity, Cursor, and Claude) interacting with this codebase.

## Directory Structure

- **`/docs/`**: Long-term architectural context, roadmap, and steering principles.
- **`/specs/`**: Functional requirements and technical specifications.
- **`glossary.md`**: Project-specific terminology to prevent semantic drift.
- **`.antigravity.json`**: Configuration for the Antigravity agent.
- **`.cursorrules`**: Context-specific rules for the Cursor IDE.
- **`CLAUDE.md`**: Operations and style guides for Claude-based agents.
- **`GEMINI.md`**: Context and reasoning instructions for Gemini-based agents.
- **`HUMAN.md`**: Workflow and roles for the Human-in-the-Loop processes.

## Why this exists?

In modern software development (2026+), managing **Agentic Context** is as critical as managing source code. By keeping these files structured in `.ai/`, we ensure that:
1. **Consistency**: All AI tools use the same rules and definitions.
2. **Persistence**: Decisions and constraints are documented for future agents.
3. **Efficiency**: Agents don't have to guess or rediscover the architect's intent.

---

> [!TIP]
> When starting a new task, tell your agent to "Read the .ai manifest" to ensure it has the latest context.

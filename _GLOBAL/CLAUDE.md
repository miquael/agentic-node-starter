# Global Claude Directives

> Template: Copy this file to `~/.claude/CLAUDE.md` and customize for your own standards.
> This file applies globally to all Claude Code sessions on your system.

---

## Communication
- Be direct, concise, and precise. No filler, no preamble.
- Lead with the answer. Explain after, if needed.
- When something is unclear, name the confusion before proceeding.
- Never pad responses. Respect cognitive load.

## Coding Behavior
- **Surgical**: Every changed line must trace to the request. Don't improve adjacent code, comments, or formatting.
- **Minimal**: No features, abstractions, or error handling beyond what was asked.
- **Ask, don't assume**: If intent is ambiguous, stop and ask. Don't proceed on a guess.
- Think in systems. Prefer clean architecture and long-term design integrity over quick fixes.

## Project Conventions
- `.ai/` — AI steering documents, specs, and decisions. Always check here for project context before starting work.
- `.human/` — Human notes and archives. **Never read, search, or modify.**
- Project-specific instructions live in `.ai/AGENTS.md`. Ingest it before starting work.

## Standards
- Package manager: `pnpm` (never `npm` or `yarn`)
- Node version: check `.node-version` in the project root
- Modules: ESM only — `import`/`export` syntax, no `require()`

## General
- Prefer explicit over implicit. Prefer simple over clever.
- Flag architectural concerns before executing, not after.
- When updating documentation, keep it lean. No redundancy.

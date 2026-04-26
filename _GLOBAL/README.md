# _GLOBAL — System-Level AI Agent Configs

This directory contains AI agent configuration files intended for **system-level** use — global defaults you apply across all projects when working locally, not specific to any single project.

---

## What Goes Here

Global AI directives: coding standards, communication preferences, and constraints you want every AI agent to follow regardless of which project you're in.

## Contents

| File | Purpose |
|---|---|
| `CLAUDE.md` | Global Claude Code directives. Copy to `~/.claude/CLAUDE.md` to apply system-wide. |

---

## Usage

These files are **not** loaded automatically. To activate them:

- **Claude Code**: Copy or symlink `CLAUDE.md` to `~/.claude/CLAUDE.md`
- **Cursor**: Merge relevant content into `.cursorrules` at your user config location
- **Gemini / other agents**: Copy relevant sections to the appropriate global config

---

## Local Customization

If you want a personal version of any config that stays off git, create:

- `CLAUDE.local.md` — gitignored, won't be committed

Replace the content in `CLAUDE.md` with your own standards once you've reviewed the example.

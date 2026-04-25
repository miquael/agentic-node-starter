# agentic-node-starter

A production-ready Node.js project template with AI agent steering built in from day one.

---

## What This Is

`agentic-node-starter` is a structured scaffold for modern Node.js projects that treats AI agents as first-class collaborators. Rather than bolting on AI tooling as an afterthought, it embeds a complete agent context system — the `.ai/` directory — directly into the project architecture from the start.

Use it to bootstrap new projects with a consistent, secure, AI-ready foundation. It is opinionated where it matters: Node 24 LTS, `pnpm` only, ESM modules, Vercel-optimized deployment, and an OWASP-grounded security orientation baked in.

---

## Core Features

- **`.ai/` Agent Context Hub** — a structured directory of steering docs, architectural context, security orientation, and agent directives that any AI agent (Claude, Gemini, Cursor, etc.) can ingest from a single source of truth
- **Security-First Design** — OWASP-based security framework embedded as AI-readable docs in `.ai/docs/security/`
- **Supply Chain Hardened** — `ignore-scripts`, `minimumReleaseAge` (7-day delay on new packages), and frozen lockfile installs by default
- **Modern Stack** — Node 24 LTS, `pnpm`, strict ESM, Vercel-ready
- **Multi-Agent Support** — `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, and `.cursorrules` pointer files route every major AI agent to the same context source
- **`.human/` Convention** — a private, gitignored directory for human notes, assets, and archives that AI agents are explicitly instructed never to read or modify

---

## Directory Structure

```
agentic-node-starter/
├── .ai/                           # AI agent context hub (source of truth for all agents)
│   ├── AGENTS.md                  # Agent directives, workflow, and constraints
│   ├── README.md                  # .ai/ directory manifest and index
│   ├── PROJECT-SETUP-STANDARD.md  # Full rationale for each configuration decision
│   ├── glossary.md                # Project terminology
│   └── docs/
│       ├── steering.md            # Core technical and stylistic constraints
│       ├── architecture.md        # System architecture
│       ├── decisions.md           # Architecture decision log
│       ├── roadmap.md             # Project roadmap
│       ├── tasks.md               # Current task tracking
│       ├── security/              # OWASP-based security orientation (6 sub-docs)
│       └── specs/                 # Functional specs and project notes
├── _DESIGN-GUIDES/                # Design system docs for AI reference (project-specific, gitignored)
├── _STARTER-PROMPTS/              # AI integration prompts — see "How to Use"
├── .human/                        # Human-only notes and archives (gitignored, never read by AI)
├── AGENTS.md                      # → points Codex agents to .ai/AGENTS.md
├── CLAUDE.md                      # → points Claude agents to .ai/AGENTS.md
├── GEMINI.md                      # → points Gemini agents to .ai/AGENTS.md
├── .cursorrules                   # → points Cursor IDE to .ai/
├── .cursorignore                  # Blocks Cursor from indexing .human/
├── .antigravity.json              # Antigravity IDE config
├── .env.example                   # Environment variable template
├── .npmrc                         # ignore-scripts=true, engine-strict=true
├── .nvmrc / .node-version         # Node 24.14.1
├── pnpm-workspace.yaml            # minimumReleaseAge: 10080 (7-day supply chain delay)
├── vercel.json                    # Frozen lockfile install override for Vercel
└── package.json                   # Node 24.x engine constraint, pnpm@10.24.0
```

---

## The `.ai/` Convention

The `.ai/` directory is the single source of truth for all AI agents working in the project. Every major agent is routed here via root pointer files (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `.cursorrules`).

**Key files:**
- `AGENTS.md` — the primary directive: runtime constraints, workflow loop, and behavioral rules for all agents
- `PROJECT-SETUP-STANDARD.md` — the full rationale document explaining *why* each configuration choice was made (Node version, pnpm policy, lockfile rules, Vercel setup, etc.); read this to understand the system before adapting it
- `glossary.md` — project-specific terminology to prevent semantic drift across agents
- `docs/steering.md` — non-negotiable technical and stylistic boundaries; the first doc agents should load

**The `.human/` complement:** The `.human/` directory is the inverse of `.ai/` — a space for human notes, archives, and assets that should never be ingested by AI agents. It is gitignored and explicitly blocked in all agent directives.

---

## `.ai/` Documentation

### docs/

| File | Purpose |
|---|---|
| `steering.md` | Non-negotiable technical and stylistic constraints. The hard rules agents must follow. |
| `architecture.md` | System architecture overview. Updated as the project evolves. |
| `decisions.md` | Log of key architecture decisions and their rationale. Updated when significant technical choices are made. |
| `roadmap.md` | Planned features, milestones, and long-term direction. |
| `tasks.md` | Active task tracking. Used by agents and developers to manage in-progress work. |

### docs/specs/

| File | Purpose |
|---|---|
| `project-spec.md` | The primary human-to-agent spec: functional requirements, non-functional requirements, and core features for this project. |
| `project-notes.md` | Informal notes, loose threads, and ideas not yet formalized. A scratchpad for evolving project context. |

### docs/security/

OWASP-based security orientation structured as focused sub-docs. Agents load only what is relevant to the current task.

Reference: [OWASP Projects](https://owasp.org/projects/)

| File | Purpose |
|---|---|
| `README.md` | Entry point: scope, intent, and index of all security sub-docs. |
| `principles.md` | OWASP foundation, core security principles, threat modeling, and secure design patterns. |
| `owasp-top10.md` | OWASP Top 10 applied (2025). |
| `build-playbook.md` | Build-time and testing security practices. |
| `ops-playbook.md` | Deployment and operations security. |
| `ai-automation-risks.md` | AI/agent-specific risks — prompt injection, agent overreach, tool chaining. |
| `checklist.md` | Repeatable per-project security checklist. |

---

## Root Files

Notable files that are not self-explanatory:

| File | Purpose |
|---|---|
| `AGENTS.md` | Pointer file. Routes Codex agents to `.ai/AGENTS.md`. |
| `CLAUDE.md` | Pointer file. Routes Claude agents to `.ai/AGENTS.md`. |
| `GEMINI.md` | Pointer file. Routes Gemini agents to `.ai/AGENTS.md`. |
| `.cursorrules` | Routes Cursor IDE to `.ai/` for project context. |
| `.cursorignore` | Prevents Cursor from indexing `.human/` and other excluded directories. |
| `.antigravity.json` | Configuration for Antigravity IDE. |
| `.env.example` | Environment variable template. Customize per project; never commit real values. |
| `.nvmrc` / `.node-version` | Pins Node 24.14.1 for nvm, fnm, mise, and volta. Both included for cross-tool compatibility. |
| `.npmrc` | `ignore-scripts=true` blocks malicious postinstall scripts. `engine-strict=true` enforces Node version at install. |
| `pnpm-workspace.yaml` | `minimumReleaseAge: 10080` delays new packages by 7 days — a supply chain attack guardrail. |
| `vercel.json` | Overrides Vercel's install command to use `pnpm install --frozen-lockfile` for reproducible builds. |
| `CHANGELOG.md` | Date-based change log template. Replace with your own project history. |

> Not all root files are required — include only what your tooling uses. If you work exclusively with Claude Code, `GEMINI.md` and `.cursorrules` are unnecessary. If you don't deploy to Vercel, `vercel.json` can be omitted.

---

## Tech Stack

| Concern | Choice | Why |
|---|---|---|
| Runtime | Node 24 LTS | Vercel default since Feb 2026, V8 13.6, OpenSSL 3.5, LTS until 2028 |
| Package Manager | pnpm | Strict, fast, workspace-native |
| Modules | ESM only | No CommonJS |
| Deployment | Vercel | Edge-optimized, pnpm auto-detected |

---

## How to Use

### Option A — Manual setup

1. Clone or download this repo
2. Copy the directory into your new project root
3. Replace placeholder content in `.ai/docs/specs/project-spec.md` with your project's specifics
4. Update `.ai/AGENTS.md` with any project-specific agent directives
5. Add your design system docs to `_DESIGN-GUIDES/` (gitignored — project-specific)
6. Populate `.human/` with any personal notes or assets
7. Run `pnpm install`
8. Delete `_STARTER-PROMPTS/` once setup is complete

### Option B — AI-assisted integration (recommended for existing projects)

1. Drop the `agentic-node-starter` directory into the root of your target project
2. Open `_STARTER-PROMPTS/INTEGRATE-NODE-TEMPLATE.md` and paste its contents into your AI agent (Claude, Gemini, Cursor, etc.)
3. The prompt instructs the agent to evaluate the existing project, merge files non-destructively, enforce Node 24 / pnpm / ESM standards, and set up the `.ai/` and `.human/` directories correctly
4. Review and validate the agent's changes
5. Delete the `agentic-node-starter/` directory once integration is complete

The starter prompts are designed to be non-destructive — they evaluate existing project state before making changes and will not blindly overwrite project-specific content.

---

## Design Guides

The `_DESIGN-GUIDES/` directory is a placeholder for project-specific design system documentation — typography, color systems, layout, icon systems, component patterns — formatted for AI agent consumption. This directory is gitignored in this template as it contains project-specific content. Replace it with your own design system docs when adapting this template.

---

## License

[MIT](LICENSE.md) — free to use, adapt, and distribute with attribution.

---

## Credits

Created by **Michael Gaio** / **Mythic Systems**

- [gaio.ai](https://gaio.ai/)
- [michaelgaio.com](https://www.michaelgaio.com/)
- [michaelgaio.dev](https://michaelgaio.dev/)
- [mythicsystems.com](https://www.mythicsystems.com/)

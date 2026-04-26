# agentic-node-starter

A production-ready Node.js project template with AI agent steering built in from day one.

---

## What This Is

`agentic-node-starter` is a structured scaffold for modern Node.js projects that treats AI agents as first-class collaborators. Rather than bolting on AI tooling as an afterthought, it embeds a complete agent context system — the `.ai/` directory — directly into the project architecture from the start.

Use it to bootstrap new projects with a consistent, secure, AI-ready foundation. It is opinionated where it matters: Node 24 LTS, `pnpm` only, ESM modules, Vercel-optimized deployment, and an OWASP-grounded security orientation baked in.

---

## Core Features

- **`.ai/` Agent Context Hub** — a structured directory of steering docs, architectural context, security orientation, and agent directives that any AI agent (Codex, Claude, Gemini, Cursor, etc.) can ingest from a single source of truth
- **Security-First Design** — OWASP-based security framework embedded as AI-readable docs in `.ai/docs/security/`
- **Supply Chain Hardened** — `ignore-scripts`, `minimumReleaseAge` (7-day delay on new packages), and frozen lockfile installs by default
- **Modern Stack** — Node 24 LTS, `pnpm`, strict ESM, Vercel-ready
- **Multi-Agent Support** — `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, and `.cursorrules` pointer files route every major AI agent to the same context source
- **`.ai/` / `.human/` Separation** — `.ai/` is the AI's dedicated context space; `.human/` is its inverse: a private, gitignored directory for personal notes, drafts, and archives that AI agents are explicitly blocked from reading. Keeping them separate ensures agents work only from intentionally structured context — not raw human scratchpad content.

---

## Directory Structure

```
agentic-node-starter/
├── .ai/                           # AI agent context hub (source of truth for all agents)
│   ├── AGENTS.md                  # Agent directives, workflow, and constraints
│   ├── README.md                  # .ai/ directory manifest and index
│   ├── PROJECT-SETUP-STANDARD.md  # Full rationale for each configuration decision
│   ├── DOMAIN-LANGUAGE.md         # Project terminology and shared language
│   └── docs/
│       ├── STEERING.md            # Core technical and stylistic constraints
│       ├── ARCHITECTURE.md        # System architecture
│       ├── DECISIONS.md           # Architecture decision log
│       ├── ROADMAP.md             # Project roadmap
│       ├── TASKS.md               # Current task tracking
│       ├── SCHEMA.md              # Data models and API contracts
│       ├── security/              # OWASP-based security orientation (6 sub-docs)
│       └── specs/                 # Functional specs and project notes
├── _DESIGN-GUIDES/                # Generic design guide committed; add project-specific guides here (gitignored)
├── _SEO_AEO_GUIDES/               # SEO & AEO reference guide — practices, llms.txt, structured data, Next.js recommendations
├── _GLOBAL/                       # System-level AI agent configs — e.g. copy CLAUDE.md to ~/.claude/CLAUDE.md
├── _STARTER-PROMPTS/              # AI integration prompts — see "How to Use"
├── .human/                        # Human-only notes and archives (gitignored, never read by AI)
├── llms.txt                       # AI discovery file — served at /llms.txt for AI crawlers and agents
├── robots.txt                     # Crawler directives — allows all bots by default, AI-bot entries included
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
- `DOMAIN-LANGUAGE.md` — project terminology and shared language to prevent semantic drift across agents
- `docs/STEERING.md` — non-negotiable technical and stylistic boundaries; the first doc agents should load

**The `.human/` complement:** The `.human/` directory is the inverse of `.ai/` — a space for human notes, archives, and assets that should never be ingested by AI agents. It is gitignored and explicitly blocked in all agent directives.

---

## `.ai/` Documentation

### docs/

| File | Purpose |
|---|---|
| `STEERING.md` | Non-negotiable technical and stylistic constraints. The hard rules agents must follow. |
| `ARCHITECTURE.md` | System architecture overview. Updated as the project evolves. |
| `DECISIONS.md` | Log of key architecture decisions and their rationale. Updated when significant technical choices are made. |
| `ROADMAP.md` | Planned features, milestones, and long-term direction. |
| `TASKS.md` | Active task tracking. Used by agents and developers to manage in-progress work. |
| `SCHEMA.md` | Data model and API contract definitions. |

### docs/specs/

| File | Purpose |
|---|---|
| `PROJECT-SPEC.md` | The primary human-to-agent spec: functional requirements, non-functional requirements, and core features for this project. |
| `PROJECT-NOTES.md` | Informal notes, loose threads, and ideas not yet formalized. A scratchpad for evolving project context. |

### docs/security/

OWASP-based security orientation structured as focused sub-docs. Agents load only what is relevant to the current task.

Reference: [OWASP Projects](https://owasp.org/projects/)

| File | Purpose |
|---|---|
| `README.md` | Entry point: scope, intent, and index of all security sub-docs. |
| `PRINCIPLES.md` | OWASP foundation, core security principles, threat modeling, and secure design patterns. |
| `OWASP-TOP10.md` | OWASP Top 10 applied (2025). |
| `BUILD-PLAYBOOK.md` | Build-time and testing security practices. |
| `OPS-PLAYBOOK.md` | Deployment and operations security. |
| `AI-AUTOMATION-RISKS.md` | AI/agent-specific risks — prompt injection, agent overreach, tool chaining. |
| `CHECKLIST.md` | Repeatable per-project security checklist. |

---

## Root Files

Notable files that are not self-explanatory:

| File | Purpose |
|---|---|
| `llms.txt` | AI discovery file. Served at `/llms.txt` — summarizes your site for AI crawlers and agents. Populate before deploying. |
| `robots.txt` | Crawler directives. Allows all bots by default. Update the `Sitemap:` URL before deploying. |
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

> Not all root files are required — include only what your tooling uses. If you work exclusively with Claude Code, `GEMINI.md`, `.antigraviry.json`, and `.cursorrules` are unnecessary. If you don't deploy to Vercel, `vercel.json` can be omitted.

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
3. Replace placeholder content in `.ai/docs/specs/PROJECT-SPEC.md` with your project's specifics
4. Update `.ai/AGENTS.md` with any project-specific agent directives
5. Add your design system docs to `_DESIGN-GUIDES/`
6. Populate `.human/` with any personal notes or assets
7. Populate `llms.txt` with your real project name, description, and page list; update the `Sitemap:` URL in `robots.txt`
8. Run `pnpm install`
9. Delete `_STARTER-PROMPTS/` once setup is complete — or keep `SEO-AEO-SETUP.md` to run once the project has real content

### Option B — AI-assisted integration (recommended for existing projects)

1. Drop the `agentic-node-starter` directory into the root of your target project
2. Open `_STARTER-PROMPTS/INTEGRATE-NODE-STARTER.md` and paste its contents into your AI agent (Codex, Claude, Gemini, Cursor, etc.)
3. The prompt instructs the agent to evaluate the existing project, merge files non-destructively, enforce Node 24 / pnpm / ESM standards, and set up the `.ai/` and `.human/` directories correctly
4. Review and validate the agent's changes
5. Delete the `agentic-node-starter/` directory once integration is complete

The starter prompts are designed to be non-destructive — they evaluate existing project state before making changes and will not blindly overwrite project-specific content.

After integration, populate `llms.txt` with your real project description and page list, and update the `Sitemap:` URL in `robots.txt`. Use `_STARTER-PROMPTS/SEO-AEO-SETUP.md` to run a full SEO/AEO audit once the project has real content.

---

## Design Guides

The `_DESIGN-GUIDES/` directory is a placeholder for project-specific design system documentation — typography, color systems, layout, icon systems, component patterns — formatted for AI agent consumption. Currently includes a generic best 2026 Node.js design principles doc. Replace or add your own design system docs here.

---

## SEO & AEO Guides

The `_SEO_AEO_GUIDES/` directory contains a reference guide covering modern SEO and AEO (AI Engine Optimization) practices as of 2026 — structured data, `llms.txt`, `robots.txt`, OpenGraph meta, semantic HTML, Core Web Vitals, and when to add Next.js for public-facing pages.

Two template files are included at the project root and should be populated before deploying:
- `llms.txt` — AI discovery file, served at `/llms.txt`
- `robots.txt` — crawler directives, served at `/robots.txt`

A ready-to-use AI audit prompt is available at `_STARTER-PROMPTS/SEO-AEO-SETUP.md`.

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

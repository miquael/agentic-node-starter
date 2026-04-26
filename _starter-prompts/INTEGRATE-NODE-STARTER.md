# Integrate __NODE-PROJECT-TEMPLATE

I have dropped the `__NODE-PROJECT-TEMPLATE` directory (and all its contents) into the root of this project. Your job is to integrate these template files into the existing project structure to standardize it for **Node 24.14.1**, **strict pnpm**, and **Vercel-optimized deployment**.

Some of these files may already exist in this project. Some may be new. You must evaluate each one and merge or create as needed — do not blindly overwrite existing project-specific content.

---

## What We Are Doing and Why

We are standardizing this project's runtime, package management, security posture, and AI agent context to a proven, battle-tested baseline. This pins the project to Node 24 LTS (Vercel's default since Feb 2026), blocks supply-chain attacks via malicious postinstall scripts, and ensures every AI agent (Claude, Gemini, Cursor, etc.) reads from a single source of truth.

---

## File Reference (What Each File Does)

### Root — Required
| File | Purpose |
|---|---|
| `package.json` | Must have `"engines": { "node": "24.x" }` and `"packageManager": "pnpm@10.24.0"`. The `24.x` syntax is required for Vercel compatibility (see below). |
| `.nvmrc` | Pins local Node version to `24.14.1` for nvm users. |
| `.node-version` | Pins local Node version to `24.14.1` for fnm/mise/volta users. |
| `.npmrc` | Sets `engine-strict=true` and `ignore-scripts=true`. Hardens security. |
| `pnpm-workspace.yaml` | Sets `minimumReleaseAge: 10080` (7-day delay on new packages). Supply-chain guardrail. |
| `.gitignore` | Standard ignores. **Do NOT remove** any existing entries. Only add missing ones from the template. Ensure `.human` is listed. |
| `.editorconfig` | Enforces consistent formatting (2-space indent, UTF-8, LF line endings). |
| `AGENTS.md` | Root pointer file. Points Codex (or general) agents to `.ai/AGENTS.md`. |
| `CLAUDE.md` | Root pointer file. Points Claude agents to `.ai/AGENTS.md`. |
| `GEMINI.md` | Root pointer file. Points Gemini agents to `.ai/AGENTS.md`. |
| `.cursorrules` | Root pointer file. Points Cursor IDE to `.ai/README.md` and `.ai/.cursorrules`. |
| `.cursorignore` | Blocks Cursor IDE from indexing `.human/`. |
| `CHANGELOG.md` | Simple date-based changelog. Create if missing, do not overwrite if it exists. |

### Root — Optional
| File | Purpose |
|---|---|
| `vercel.json` | Overrides Vercel install/build commands to use `pnpm install --frozen-lockfile`. Only needed if deploying to Vercel. |
| `.env.example` | Template for environment variables. Customize to this project's needs. |
| `LICENSE.md` | License file. Do not overwrite if one already exists. |

### `.ai/` Directory — Agent Context (Required)
| File / Dir | Purpose |
|---|---|
| `AGENTS.md` | **Single source of truth** for all AI agent directives: runtime constraints, pnpm rules, workflow loop, and the `.human/` ignore rule. |
| `README.md` | Manifest describing the `.ai/` directory structure. |
| `.cursorrules` | Cursor-specific IDE behavior rules. |
| `glossary.md` | Project-specific terminology to prevent AI semantic drift. Customize per project. |
| `PROJECT-SETUP-STANDARD.md` | Full reference doc explaining *why* each config choice was made. Read this for context. |
| `docs/` | Architectural context, steering constraints, decisions, tasks, roadmap. |
| `docs/specs/` | Functional requirements and technical specifications. |

### `.human/` Directory — Human-Only Archive (Required)
| File / Dir | Purpose |
|---|---|
| `.human/README.md` | Instructs AI agents to **never** read, ingest, or modify anything in this directory. |
| `.human/archive/` | Drop zone for legacy docs, old iterations, and out-of-context notes. |

> **Critical**: `.human/` must be added to `.gitignore` and `.cursorignore`. AI agents must never access it.

---

## Why `"24.x"` in package.json (not `"24.14.1"` or `"^24.14.1"`)

Vercel's Node 24 instances run their own patch version (e.g., `24.14.1`). Combined with `engine-strict=true` in `.npmrc`, using an exact version or caret range causes pnpm to reject the install if there is any mismatch. `"24.x"` is Vercel's preferred syntax: it locks to the Node 24 major branch while allowing any patch version within it. Local development is still pinned to exactly `24.14.1` via `.nvmrc` and `.node-version`.

---

## Integration Sequence

Execute in this order:

### Step 1 — Read Context
- Read `__NODE-PROJECT-TEMPLATE/README.md` to understand what __NODE-PROJECT-TEMPLATE is.
- Read `__NODE-PROJECT-TEMPLATE/.ai/PROJECT-SETUP-STANDARD.md` to understand the full rationale.
- Read `__NODE-PROJECT-TEMPLATE/.ai/AGENTS.md` to understand the agent directive format.
- Scan the existing project to understand what already exists.

### Step 2 — Enforce pnpm
- If `package-lock.json` exists, delete it.
- If `yarn.lock` exists, delete it.
- Ensure `package.json` has `"packageManager": "pnpm@10.24.0"`.
- Ensure `.npmrc` has `ignore-scripts=true` and `engine-strict=true`.
- Ensure `pnpm-workspace.yaml` has `minimumReleaseAge: 10080`.

### Step 3 — Pin Node 24.14.1
- Set `.nvmrc` to `24.14.1`.
- Set `.node-version` to `24.14.1`.
- Set `engines.node` to `"24.x"` in `package.json`.

### Step 4 — Set Up Agent Context (`.ai/`)
- If `.ai/` does not exist, copy the entire directory from the template.
- If `.ai/` already exists, merge carefully:
  - Ensure `AGENTS.md` exists and contains the consolidated directives (not separate CLAUDE/GEMINI/HUMAN files inside `.ai/`).
  - If separate `.ai/CLAUDE.md`, `.ai/GEMINI.md`, or `.ai/HUMAN.md` files exist, merge their unique content into `AGENTS.md` and delete them.
  - If `.ai/specs/` exists separately from `.ai/docs/`, move it into `.ai/docs/specs/`.
  - Ensure `.ai/README.md` accurately reflects the final directory structure.
- Ensure root `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` are pointer files to `.ai/AGENTS.md`.
- Ensure `.cursorrules` and `.cursorignore` are in place.

### Step 5 — Set Up `.human/`
- Create `.human/` and `.human/archive/` if they don't exist.
- Place the `README.md` inside `.human/` (the one that says "AI Agents: STOP").
- Add `.human` to `.gitignore` (under a `# Human` heading).
- Add `.human/` and `.human/*` to `.cursorignore`.

### Step 6 — Merge Supporting Files
- Merge `.gitignore` entries from the template. **Never remove existing entries**, only add.
- Copy `.editorconfig` if missing or outdated.
- Copy `.env.example` if missing (customize if one already exists).
- Copy `CHANGELOG.md` if missing. Do not overwrite.
- Copy `vercel.json` if the project deploys to Vercel.

### Step 7 — Clean Install
- Delete `node_modules/` completely.
- Run `pnpm install` to generate a clean `pnpm-lock.yaml`.
- Verify the install succeeds without errors.

### Step 8 — Delete the Template
- Remove the `__NODE-PROJECT-TEMPLATE/` directory and `_starter-prompts/` directory from the project root. They are no longer needed.

---

## Final Checklist

- [ ] `package.json` has `"node": "24.x"` and `"packageManager": "pnpm@10.24.0"`
- [ ] `.nvmrc` = `24.14.1`
- [ ] `.node-version` = `24.14.1`
- [ ] `.npmrc` has `engine-strict=true` and `ignore-scripts=true`
- [ ] `pnpm-workspace.yaml` has `minimumReleaseAge: 10080`
- [ ] No `package-lock.json` or `yarn.lock` exists
- [ ] `.ai/AGENTS.md` exists with consolidated directives
- [ ] Root `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md` point to `.ai/AGENTS.md`
- [ ] `.human/` exists with its README, is in `.gitignore`, and is in `.cursorignore`
- [ ] `pnpm install` completes successfully

Once this is all completed and project is stable, I will delete `__NODE-PROJECT-TEMPLATE/`

---

**Wait to execute. Ask questions first if anything is unclear about the existing project state.**

---

> **Note**: Once complete, don't forget to remind user to install Node 24.14.1 locally (e.g., `nvm install 24.14.1`) and then run `pnpm install` once the integration is complete to ensure local environment matches the new project standards.

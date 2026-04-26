# Domain Language & Shared Terminology

> A living reference for shared language across this project and its AI agents. Prevents semantic drift, aligns intent, and ensures consistent communication between human contributors and AI collaborators.

---

## How to Use This File
- Add terms as they emerge — don't wait until the glossary is "complete"
- Prefer precision over brevity in definitions
- Flag terms that overlap with common usage but carry project-specific meaning
- AI agents: consult this file when terminology is ambiguous

---

## Core Architecture

- **Agentic Context Layer**: The `.ai/` directory and its contents. The single source of truth for all AI agents working in the project — directives, steering constraints, documentation, and specifications.
- **Steering Document**: A non-negotiable set of architectural and stylistic constraints (`STEERING.md`). Agents must comply; humans must not override casually.
- **Pointer File**: A root-level file (`CLAUDE.md`, `AGENTS.md`, `GEMINI.md`, `.cursorrules`) that routes an AI agent to the canonical context in `.ai/`. Contains no substantive directives itself.
- **Human Archive**: The `.human/` directory. Off-limits to all AI agents. Stores personal notes, archived files, and out-of-context materials.

---

## Technical Stack

- **Strict pnpm**: Use of `pnpm` exclusively, enforced via `.npmrc`, `pnpm-workspace.yaml`, and `package.json` engine constraints. No mixing with `npm` or `yarn`.
- **ESM (ES Modules)**: The JavaScript module format used throughout. `import`/`export` syntax only. No `require()` or `module.exports`.
- **Frozen Lockfile Install**: `pnpm install --frozen-lockfile` — installs exactly what is in `pnpm-lock.yaml` without updating it. Used in CI and Vercel.
- **Supply Chain Delay**: `minimumReleaseAge: 10080` — pnpm will not install packages published less than 7 days ago. Protects against supply-chain attacks.

---

## Domain-Specific Terms

> Replace or extend this section with terminology specific to your project's domain.

- **Spec**: Ground truth functional requirements, defined in `docs/specs/PROJECT-SPEC.md`.
- **Schema**: Data structure definitions for the project's models and API contracts, defined in `docs/SCHEMA.md`.
- **ADR (Architecture Decision Record)**: A logged decision with status, rationale, and alternatives considered. Maintained in `docs/DECISIONS.md`.

---

## Naming Conventions

- Standard scaffold docs use **UPPERCASE** names (e.g., `ARCHITECTURE.md`, `DECISIONS.md`). This visually distinguishes template structure from project-specific content.
- Platform-specific config files use their required names (e.g., `.cursorrules`, `.antigravity.json`).
- Project-specific content in `docs/specs/` follows the same UPPERCASE convention (`PROJECT-SPEC.md`, `PROJECT-NOTES.md`).

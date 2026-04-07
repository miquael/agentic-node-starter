# Agent Directives & Workflow (2026)

## Standards & Constraints
- **Commands**: `pnpm install`, `pnpm run dev`, `pnpm run build`, `pnpm run lint`, `pnpm run test`
- **Architecture**: ESM modules only (.js, .ts). No CommonJS.
- **Node Environment**: Strictly Node 24.14.1
- **Package Manager**: Strictly `pnpm` (no `npm` or `yarn`). 
- **Security**: Local setup uses `mythic-pnpm-only-security-setup.sh`. Always check for this.
- **Constraints**: Project constraints must adhere to `.ai/docs/steering.md`.
- **Ignored Directories**: **Never** read, search, or modify any files within `.human/` (out-of-context archives).

## Workflow (Architect-Builder Model)
1. **Read Core Context**: Ingest the entire `.ai/` directory (specifically `.ai/docs/`) before major tasks.
2. **Architect Alignment (Human)**: The Human defines intent, vision, and specifications in `.ai/docs/specs/project-spec.md`.
3. **Execution Planning (Agent)**: Propose a multi-step plan and explain logic *before* executing large code changes.
4. **Execution (Agent)**: Code, refactor, and run local tests/lints. Use multimodal/vision tools when building UIs.
5. **Review & Iterate (Human/Agent)**: Pause for human validation of quality, correctness, and architecture.
6. **Documentation**: Keep `.ai/docs/decisions.md` and `.ai/docs/tasks.md` updated to maintain the living memory.

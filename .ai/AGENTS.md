# Agent Directives & Workflow

## Standards & Constraints
- **Commands**: `pnpm install`, `pnpm run dev`, `pnpm run build`, `pnpm run lint`, `pnpm run test`
- **Architecture**: ESM modules only (.js, .ts). No CommonJS.
- **Node**: 24.14.1
- **Package Manager**: `pnpm` only (no `npm` or `yarn`)
- **Constraints**: Adhere to `.ai/docs/STEERING.md`.

## Workflow (Architect-Builder Model)
1. **Read Core Context**: See `.ai/README.md` for a full index of this directory. Ingest relevant files in `.ai/docs/` before major tasks.
2. **Architect Alignment**: Human defines intent, vision, and specs in `.ai/docs/specs/PROJECT-SPEC.md`.
3. **Execution Planning**: Propose a multi-step plan and explain logic *before* executing large code changes.
4. **Execution**: Code, refactor, and run local tests/lints.
5. **Review & Iterate**: Pause for human validation of quality, correctness, and architecture.
6. **Documentation**: When updating files in `.ai/docs/`, keep files lean and concise. Keep `.ai/docs/DECISIONS.md` and `.ai/docs/TASKS.md` updated.

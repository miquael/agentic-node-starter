# Project Steering & Principles

## Core Mandates
- **Package Management**: Use **pnpm only**. Never use `npm` or `yarn`. 
- **Module System**: Strict **ESM (ES Modules)**. No CommonJS.
- **Node Version**: Check `.node-version` for current target.
- **Security**: All projects must ensure that local `npm` calls are redirected to `pnpm`.

## Architecture Principles
1. **Composition Over Inheritance**: Prefer mixing functionality via hooks or utilities.
2. **Deterministic Outputs**: Pure functions wherever possible for easier testing.
3. **Lazy Loading**: High performant design; only load what is needed.
4. **Agentic-First Docs**: Keep `.ai/docs/` updated as the codebase evolves.

## Coding Style
- **Naming**: Use descriptive, semantic-first variable and function names.
- **Comments**: Focus on "Why," not "What." Use JSDoc for complex logic.
- **Formatting**: Standardize via `.editorconfig` and `prettier`.

### Prohibitions (What we NEVER do)
- No `any` type in TypeScript.
- No direct manipulation of the DOM unless in a dedicated "low-level" module.
- No secret keys in source code (always use `.env`).

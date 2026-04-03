# Claude Agent Guide (2026)

This project uses Claude for coding tasks via various interfaces (Claude Dev, Cline, Claude Desktop).

## Standard Commands
- **Install**: `pnpm install`
- **Develop**: `pnpm run dev`
- **Build**: `pnpm run build`
- **Lint**: `pnpm run lint`
- **Test**: `pnpm run test`

## Architecture & Style
- **Modules**: ESM (ES Modules).
- **Package Manager**: Strict `pnpm`.
- **Structure**: See `.ai/README.md` for the context manifest.
- **Constraints**: Follow `.ai/docs/steering.md` for project-specific rules.

## Error Handling
- Use structured error responses.
- Don't assume libraries are available; check `package.json`.

---
*Created as part of the NODE-PROJECT-TEMPLATE v1.0.0*

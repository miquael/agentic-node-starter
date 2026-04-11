# Architecture Decision Records (ADR)

## ADR-001: Strict pnpm Usage
- **Status**: [ACCEPTED]
- **Reasoning**: NPM leads to dependency drift and is less secure locally. `pnpm` ensures consistency across Vercel and local dev.
- **Alternatives Considered**: Yarn (discarded — lacks pnpm-only lock features).

## ADR-002: Agentic Context (.ai/) Hub
- **Status**: [ACCEPTED]
- **Reasoning**: Dedicated directory for rules and specs avoids root clutter while requiring root-level pointers.
- **Alternatives Considered**: Keeping `docs/` in the root.

## ADR-003: Node 24 LTS Baseline (upgraded from Node 22)
- **Status**: [ACCEPTED]
- **Date**: 2026-04-07
- **Reasoning**: Node 24 became Vercel's default in Feb 2026, entered LTS Oct 2025. Provides V8 13.6 (~30% faster), OpenSSL 3.5, mature ESM, LTS until 2028. Fighting Vercel's default was creating friction.
- **Alternatives Considered**: Node 22 LTS (valid but ends 2027; no longer Vercel's default).
- **Migration Notes**: `engines.node` → `"24.x"`, `.nvmrc` / `.node-version` → `24.14.1`.

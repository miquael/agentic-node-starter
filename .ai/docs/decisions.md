# Architecture Decision Records (ADR)

This log tracks the **Why** behind architectural choices to prevent future agents from unknowingly reversing critical decisions.

## ADR-001: Strict pnpm Usage
- **Status**: [ACCEPTED]
- **Proposer**: AI Agent
- **Reasoning**: NPM can lead to "dependency drift" and is less secure in local contexts. Using `pnpm` ensures consistency across Vercel and local dev.
- **Alternatives Considered**: Yarn (discarded due to lack of standard pnpm-only lock features in template).

## ADR-002: Agentic Context ( .ai/ ) Hub
- **Status**: [ACCEPTED]
- **Proposer**: User
- **Reasoning**: Having a dedicated, clean directory for "Rules" and "Specs" is more organizational than cluttering the root, but requires root-level pointers.
- **Alternatives Considered**: Keeping docs/ in the root.

## ADR-003: Node 24 LTS Baseline (upgraded from Node 22)
- **Status**: [ACCEPTED]
- **Date**: 04/07/2026
- **Proposer**: User
- **Reasoning**: Node 24 became Vercel's default in Feb 2026 and entered LTS in Oct 2025. It provides V8 13.6 (up to 30% faster), OpenSSL 3.5 (stricter security defaults), mature ESM support, and LTS until 2028. For a forward-looking template, fighting Vercel's default was creating friction.
- **Alternatives Considered**: Staying on Node 22 LTS (valid but shorter-lived, ends 2027; no longer Vercel's default).
- **Migration Notes**: `engines.node` → `"24.x"`, `.nvmrc` / `.node-version` → `24.14.1`. The `"24.x"` pattern follows the same Vercel-compatible convention previously used for `"22.x"`.

---
*Created as part of the NODE-PROJECT-TEMPLATE v1.0.0*

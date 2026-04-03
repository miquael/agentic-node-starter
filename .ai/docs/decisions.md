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

---
*Created as part of the NODE-PROJECT-TEMPLATE v1.0.0*

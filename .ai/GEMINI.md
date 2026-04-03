# Gemini Agent Guide (2026)

This project is optimized for Gemini-based agents (1.5 Pro, 2.0, and newer). 

## Context Architecture
- **Long-Context Awareness**: This project uses a deep `.ai/` directory for context. When starting a complex task, Gemini agents should ingest the entire `.ai/` directory to build a complete project mental model.
- **Steering**: Refer to [.ai/docs/steering.md](file:///.ai/docs/steering.md) for non-negotiable architectural constraints.

## Task Workflow
- **Reasoning First**: Before writing code, use your reasoning capabilities to propose a multi-step plan.
- **Multimodal Integration**: If requested to build a UI, generate images or use vision tools to validate layouts.
- **Truth Source**: Functional logic must always align with [.ai/specs/project-spec.md](file:///.ai/specs/project-spec.md).

## Operational Standards
- **Runtime**: Node.js (Latest stable).
- **Package Manager**: pnpm (strict).
- **Security**: Local setup uses `mythic-pnpm-only-security-setup.sh`. Always check for this script's presence.

---
*Optimized for Google Deepmind's Advanced Agentic Coding (Antigravity)*

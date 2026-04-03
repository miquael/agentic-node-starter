# Human-in-the-Loop Workflow (2026)

This document defines the interaction model between the **Human (Architect)** and the **AI Agent (Builder)** for this project.

## The Architect-Builder Loop

The primary operating model for this project is a strict cycle of refinement:

1.  **Idea & Intent** (Human): Define the vision and high-level goals.
2.  **Architecture Alignment** (Human/AI): Update [.ai/docs/architecture.md](file:///.ai/docs/architecture.md) to define structure.
3.  **Functional Specification** (Human/AI): Finalize requirements in [.ai/specs/project-spec.md](file:///.ai/specs/project-spec.md).
4.  **Execution Planning** (AI): AI presents a step-by-step implementation plan for approval.
5.  **Implementation** (AI): Agent codes, refactors, and runs initial unit/lint tests.
6.  **Human Review** (Human): Review code for quality, intent, and "vibe." Provide feedback.
7.  **Close the Loop** (AI): Update [.ai/docs/decisions.md](file:///.ai/docs/decisions.md) and [.ai/docs/tasks.md](file:///.ai/docs/tasks.md).
8.  **Iterate**.

## Roles & Responsibilities

### The Human (Architect)
- **Intent**: Define *what* we are building and *why*.
- **Review**: Validate that the implementation matches the vision.
- **Constraints**: Set boundaries in [.ai/docs/steering.md](file:///.ai/docs/steering.md).
- **Steering**: Keep the AI on track if it begins to "wander" technically.

### The AI Agent (Builder)
- **Execution**: Write clean, modular, and secure code.
- **Planning**: Explain logic and propose plans *before* large-scale changes.
- **Refactoring**: Continuously improve code quality during implementation.
- **Documentation**: Keep the `.ai/` context hub updated as a "living" memory.

---
*Created as part of the NODE-PROJECT-TEMPLATE v1.0.0*

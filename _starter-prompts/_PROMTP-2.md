Please perform a deep structural cleanup and optimization of this project's .ai/ (Agentic Context) directory. The goal is to aggressively reduce context-window bloat, remove generic template boilerplate, and create a highly dense, actionable "Source of Truth" for AI agents.

Execute the following steps exactly:

1. Consolidate Agent Directives (AGENTS.md)

Delete individual AI/human workflow files inside .ai/ (such as CLAUDE.md, GEMINI.md, and HUMAN.md).
Combine their core operational logic into a single, unified .ai/AGENTS.md file. Keep it dense and focused on technical execution rules (e.g., "always use pnpm", runtime versions) and the core human/AI loop.
If there are pointer files in the project root (/CLAUDE.md, /GEMINI.md), update them to point to .ai/AGENTS.md.
2. Eradicate Boilerplate Templates

Review all files in .ai/docs/ or .ai/. Identify and delete files that contain only generic template setups or empty placeholders (e.g., decisions.md, tasks.md, roadmap.md, PROJECT-SETUP-STANDARD.md). We only want active, custom logic.
Rewrite .ai/docs/steering.md to strip out philosophical filler and hypothetical scripts. Replace it strictly with the actual runtime parity constraints of this specific project.
3. Consolidate Documentation Trunks

If there is an .ai/specs/ directory separated from .ai/docs/, move specs/ completely inside docs/ (making it .ai/docs/specs/). A single documentation trunk prevents unnecessary directory hopping during AI context framing.

4. Trim the Glossary

Review .ai/glossary.md. Delete all generic programming terms (like "Model", "ESM", or "Schema").
Replace the contents with 3 to 4 highly specific, domain-related terms unique to this exact project to prevent AI hallucination.
5. Segregate Legacy Knowledge (.human/)

Create a directory at the project root called .human/ (or .human/archive/).
Move all legacy reports, old development tasks, and dead architecture records out of root docs/ or .ai/ and into this .human/ directory.
Open the project's .gitignore and append .human/ under a heading called # Explicit Context Denials. This mathematically guarantees that IDE context window tools and AI Git-tree scanners will ignore this folder, saving thousands of tokens.
6. Synchronize Manifests

Rewrite .ai/README.md (the Agent Manifest) to perfectly reflect this new, leaner file tree.
Update the root README.md to accurately point to .ai/README.md for AI context and explain that .human/ is reserved for restricted/personal archives.
# CHANGE-LOG

Dates format: MM/DD/YYYY
All notable changes to this project will be documented in this file.

---

## [04/07/2026]
### Changed
- **Node.js upgraded from 22.x to 24.x (LTS).**
- Pinned local version: `24.14.1` (`.nvmrc`, `.node-version`).
- Engine constraint: `"24.x"` (`package.json`).
- Updated all documentation: `AGENTS.md`, `PROJECT-SETUP-STANDARD.md`, `INTEGRATE-NODE-TEMPLATE.md`, `architecture.md`, and `decisions.md`.
- Rationale: Node 24 is Vercel's default since Feb 2026, offers V8 13.6 (up to 30% faster), OpenSSL 3.5 strict security, mature ESM support, and LTS until 2028.

---

## [04/06/2026]
### Added
- Standardized Project Structure initialized.
- Agent Context (`.ai/`) deployed.
- Node `22.22.2` baseline established.

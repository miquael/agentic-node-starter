# Project Architecture & Systems

## System Overview
- **Type**: Node.js Application (Vercel-ready).
- **Core Engine**: To be determined upon implementation.
- **Data Flow**: To be determined upon implementation.

## Key Components
- **Middleware**: For request handling and security headers.
- **Services**: Business logic decoupled from external interfaces.
- **Utils**: Reusable, pure functional helpers.
- **Schemas**: Data structure definitions (see `SCHEMA.md`).

## Technical Stack
- **Runtime**: Node.js (v24 LTS).
- **Deployment**: Vercel (see `vercel.json`).
- **Dependencies**: Managed via pnpm (strict pnpm only).
- **Styling**: Vanilla CSS (unless explicitly requested otherwise).

## Infrastructure
- **CI/CD**: Vercel/GitHub Actions.
- **Caching**: Local in-memory caching where applicable.


# Project Setup Standard (Node / pnpm / Vercel / Security)

This document defines the standard setup for all new projects.

Goals:
- Consistent environments across local, CI, and Vercel
- Supply-chain security
- Reproducible installs
- No mixing package managers

---

# 1 — Package Manager Policy

Use **pnpm** for all new projects. Do NOT mix package managers.

Allowed:
- pnpm
- pnpm-lock.yaml

Avoid:
- npm install for normal work
- package-lock.json in pnpm projects
- Switching between npm and pnpm mid-project

If a project uses npm instead:
- Use package-lock.json
- Use npm ci in CI
- Do not use pnpm

**Rule:** One project = one package manager.

---

# 2 — Security Baseline

## .npmrc (project root)
```ini
ignore-scripts=true
engine-strict=true
```

- `ignore-scripts` prevents malicious postinstall scripts from running automatically
- `engine-strict` fails installs if the Node version doesn't match the `engines` field in package.json

> Note: pnpm v10 also blocks dependency lifecycle scripts by default. If a package needs to run build scripts (e.g., esbuild, fsevents), use `pnpm approve-builds` or the `allowBuilds` setting in `pnpm-workspace.yaml`.

## pnpm-workspace.yaml (project root)
```yaml
minimumReleaseAge: 10080  # 7 days delay for new packages
```

- Requires pnpm >= 10.16
- Prevents installing packages published less than 7 days ago
- Protects against supply-chain attacks (malicious packages are typically caught within days)

Both files must be committed to Git so CI and Vercel use the same rules.

---

# 3 — Install Discipline

## Normal development
```bash
pnpm install
```

## Strict / CI / reproducible install
```bash
pnpm install --frozen-lockfile
```

## If using npm instead
```bash
npm ci
```

Rules:
- Do NOT use `npm install` in CI
- Do NOT regenerate lockfiles casually
- Lockfiles must be committed

---

# 4 — Lockfile Rules

Always commit:
- `pnpm-lock.yaml` (for pnpm projects)
- `package-lock.json` (for npm projects)

Generate the lockfile by running `pnpm install` after setting up the project. The lockfile ensures reproducible installs and must be committed from the start.

Never:
- Delete lockfile without reason
- Regenerate lockfile casually
- Mix pnpm-lock.yaml and package-lock.json

Lockfiles ensure:
- Reproducible installs
- CI matches local
- No dependency drift
- Protection against malicious package updates

---

# 5 — Pin Package Manager Version

In `package.json`, include:
```json
{
  "packageManager": "pnpm@10.24.0"
}
```

This ensures:
- Consistent pnpm version across all environments
- Vercel uses the correct package manager
- All contributors run the same version

---

# 6 — Pin Node Version

Include both `.nvmrc` and `.node-version` files in the project root with the same Node version:

```
22.0.0
```

`.nvmrc` is read by nvm. `.node-version` is read by other version managers (fnm, mise, volta). Including both ensures compatibility regardless of which tool contributors use.

The `engines` field in `package.json` enforces this at install time:
```json
{
  "engines": {
    "node": ">=22.0.0"
  }
}
```

Combined with `engine-strict=true` in `.npmrc`, pnpm will refuse to install if the Node version is wrong.

---

# 7 — Vercel / CI Notes

Vercel detects the package manager automatically from:
- pnpm-lock.yaml
- packageManager field in package.json

Preferred setup:
- Commit pnpm-lock.yaml
- Commit .npmrc
- Commit pnpm-workspace.yaml
- Include packageManager in package.json

Optional `vercel.json` install command override:
```json
{
  "installCommand": "pnpm install --frozen-lockfile"
}
```

Use this if you want strict dependency reproducibility on Vercel.

---

# 8 — New Project Checklist

1. Create project folder
2. Add `.npmrc`
3. Add `pnpm-workspace.yaml`
4. Add `.nvmrc` and `.node-version`
5. Set `packageManager` and `engines` in package.json
6. Run `pnpm install` to generate lockfile
7. Commit `pnpm-lock.yaml`
8. Push to GitHub
9. Deploy to Vercel
10. Confirm Vercel detects pnpm

---

# 9 — Template Files

The `__PROJECT-TEMPLATE` folder includes:

```
__PROJECT-TEMPLATE/
├── .npmrc
├── .nvmrc
├── .node-version
├── .gitignore
├── .env.example
├── .editorconfig
├── package.json
├── pnpm-workspace.yaml
├── vercel.json (optional)
├── README.md
├── LICENSE.md (optional)
└── PROJECT-SETUP-STANDARD.md
```

---

# 10 — Quick Reference Commands

## Install pnpm (if not installed)
```bash
npm install -g pnpm@10.24.0
```

## Install dependencies
```bash
pnpm install
```

## Strict install (CI / Vercel)
```bash
pnpm install --frozen-lockfile
```

## npm strict install (npm projects only)
```bash
npm ci
```

---

# 11 — Operating Principles

- One project = one package manager
- Always commit lockfiles
- Never blindly run npm install on unknown repos
- Delay new package versions (minimumReleaseAge)
- Block install scripts unless explicitly needed
- Use frozen lockfile installs in CI
- Prefer pnpm over npm
- Reproducibility > convenience
- Security > speed
- Stability > newest version

---

# End of Document
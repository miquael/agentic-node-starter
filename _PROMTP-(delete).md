okay, let's make some significant updates:
1 - i just added a bunch of new fiels to root:
> read .ai/PROJECT-SETUP-STANDARD.md - we want to get in line with this.
> see: GEMINI.md - which refers to .ai/GEMINI.md (which is a boilerplate-so we can update this when you want)
> .ai is filled with boiler plate, including .ai docs/ which is distinct from docs/ in root.  be sure to read docs/README.md - and let's consider if we should move docs/ to .ai/docs and integrate?
> see .gitignore2 - a reference to possibly update .gitignore. DO NOT REMOVE anything from .gitignore unless you know it is safe, but use .gitignore2 as reference to add or reorganize .gitignore
> i renamed and moved CHANGE-LOG.md to root
> i added: .env.example, .node-version, .nvmrc, and more ... to root
> review the new set up, and be sure all is in sync.

the goal is to standardize this project for Node 22.22.2 and strict pnpm security (Optimized for Vercel), and have a stable app with your steering docs (specs, etc) are all in place and sorted.

be sure this is all done (some of these things may already be complete):

Update package.json:
Set engines.node to "22.x" (this is the Vercel standard string: it locks to Node 22 but allows minor patches, and fixes the Vercel Node 24 auto-upgrade warning).
Pin packageManager to "pnpm@10.24.0".
Sync Local Version Files: Create/update both .nvmrc and .node-version in the root, setting them specifically to 22.22.2 (to match the Vercel production environment).
Harden Security in .npmrc: Set engine-strict=true (forces consistent Node versions across all developers) and ignore-scripts=true (prevents malicious package postinstalls).
Add Supply-Chain Guardrail: Create a pnpm-workspace.yaml with the line minimumReleaseAge: 10080 (this enforces a 7-day security delay for all new packages).
Finish the Clean Migration: Delete package-lock.json and the old node_modules, then run pnpm install to generate the final pnpm-lock.yaml.

all clear? any recommendations?

ask questions if you need to.
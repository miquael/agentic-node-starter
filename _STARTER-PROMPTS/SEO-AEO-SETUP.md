# Starter Prompt: SEO & AEO Audit + Setup

Copy and paste this prompt into your AI IDE (Cursor, Windsurf, Claude Code, etc.) to audit your project for SEO/AEO gaps and auto-generate the recommended infrastructure.

Run this **at project start** (to scaffold the baseline) or **once the project has real content** (to generate accurate structured data, llms.txt, and sitemap entries).

---

## The Prompt

```
You are an SEO and AEO (AI Engine Optimization) engineer. Audit this project and implement all missing SEO/AEO infrastructure. Follow the steps below in order.

---

STEP 1 — DETECT PROJECT TYPE

Determine whether this project is:
A) A pure Node.js backend / API / server-rendered app (Express, Fastify, Hapi, etc.)
B) A Next.js project (App Router or Pages Router)
C) A Node.js project that could benefit from adding Next.js for public-facing pages

State your finding clearly before proceeding.

---

STEP 2 — AUDIT EXISTING INFRASTRUCTURE

Check for the presence and correctness of:
- [ ] /robots.txt — exists at project root? Correct format? AI bots allowed/blocked appropriately?
- [ ] /llms.txt — exists at project root? Populated with real content or still a template?
- [ ] /llms-full.txt — exists? (optional but high-value for content sites)
- [ ] sitemap.xml — generated or served? Submitted to Search Console?
- [ ] JSON-LD structured data — present on key pages? Correct schema types?
- [ ] OpenGraph + Twitter Card meta tags — present and accurate per page?
- [ ] Canonical URLs — set on each page?
- [ ] Semantic HTML structure — proper <h1>, landmark elements, alt text?
- [ ] Server-side rendering — is content in the HTML response, or JS-only?

Report a checklist: present / missing / needs update for each item.

---

STEP 3 — IMPLEMENT MISSING ELEMENTS

Based on the audit, implement or update the following. For each item, confirm before writing files if the change is non-trivial.

### All projects (Node.js and Next.js):

1. **robots.txt** — If missing or incomplete, create/update at project root.
   - Allow all paths by default
   - Include named AI bot directives: GPTBot, ClaudeBot, PerplexityBot, GoogleOther
   - Include Sitemap: line pointing to the correct domain

2. **llms.txt** — If still a placeholder template, populate it with:
   - Real project name and one-sentence description
   - Actual page paths and descriptions based on the codebase
   - Group into logical sections (Overview, Docs, Features, etc.)

3. **Structured data (JSON-LD)** — Identify the 2–3 most applicable schema types for this project and implement them on the appropriate pages:
   - Organization or WebSite — site-wide (in root layout or <head>)
   - FAQPage — on any FAQ or Q&A section
   - Article / BlogPosting — on blog or article pages
   - Service — on service/product pages
   - SoftwareApplication — if this is a tool or app
   Use schema.org as the reference. Embed as <script type="application/ld+json"> in <head>.

4. **OpenGraph + Twitter Card meta** — Ensure every public page has:
   - og:title, og:description, og:image, og:url, og:type
   - twitter:card (summary_large_image)

5. **Semantic HTML** — Audit rendered HTML for:
   - Exactly one <h1> per page
   - Correct heading hierarchy (h1 → h2 → h3, no skipping)
   - Landmark elements: <main>, <nav>, <footer>, <article> where appropriate
   - Descriptive alt text on all images

### If Next.js (App Router):

6. **generateMetadata** — Replace any manual <meta> tags with typed generateMetadata exports in each route segment. Include: title, description, openGraph, twitter, alternates.canonical.

7. **app/sitemap.ts** — Create or update to return a MetadataRoute.Sitemap array covering all public routes. Use real URLs based on the project domain in .env.

8. **app/robots.ts** — If preferred over a static file, convert robots.txt to a programmatic route.

9. **app/llms.txt/route.ts** — Create a route handler that serves the llms.txt content as text/plain. Optionally generate it dynamically from page metadata.

### If plain Node.js:

6. **Sitemap** — Install the `sitemap` package and create a /sitemap.xml route that generates XML from your known routes. Or generate a static sitemap.xml at build time.

7. **Meta tags in templates** — Ensure all server-rendered HTML templates include the full OG + canonical meta set in <head>.

8. **Static file serving** — Confirm robots.txt and llms.txt are served correctly from the root path (not /public/robots.txt, but /robots.txt).

---

STEP 4 — REPORT

After implementation, output a summary:
- What was created or updated
- What was already correct
- Any items skipped and why
- 2–3 highest-priority remaining content/copy recommendations for AEO (answer-first structure, FAQ pages, internal linking)
```

---

## Notes on When to Run This

- **At project start**: Run it to scaffold `robots.txt`, `llms.txt`, OG meta structure, and JSON-LD templates. You'll get placeholder content that you fill in as the project develops.
- **Once content exists**: Run it again (or just Step 2–4) to populate `llms.txt` with real page descriptions, generate accurate structured data, and validate that everything is wired up correctly.
- **After adding new pages or features**: Re-run Step 2 as a quick audit to catch missing meta or schema on new routes.

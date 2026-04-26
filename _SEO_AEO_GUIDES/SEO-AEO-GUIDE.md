# SEO & AEO Guide — April 2026

Covers both traditional Search Engine Optimization (SEO) and AI Engine Optimization (AEO) — the emerging discipline of making your content legible and authoritative to AI-powered search surfaces (Google AI Overviews, Perplexity, ChatGPT Browse, Claude tools, Bing Copilot, etc.).

---

## SEO vs. AEO — What's Different in 2026

Traditional SEO optimizes for ranked blue links. AEO optimizes for being *cited* or *synthesized* by AI systems that answer questions directly — often without the user ever clicking through.

The two are complementary, not separate. Good SEO is a prerequisite for AEO. But AEO adds new requirements:

- Machine-readable structure (JSON-LD, semantic HTML)
- AI-specific discovery files (`llms.txt`)
- Answer-first content that AI can quote verbatim
- E-E-A-T signals (Experience, Expertise, Authoritativeness, Trustworthiness) — now factored into AI citation quality, not just Google ranking

---

## `llms.txt` — AI Discovery File

**What it is**: A plain Markdown file served at `/llms.txt` that summarizes your site for AI crawlers and agents. An emerging standard (proposed 2024, gaining broad adoption through 2025–2026) analogous to `robots.txt` but for AI agents rather than traditional crawlers.

**Where it lives**: Project root, served at the domain root (`https://yourdomain.com/llms.txt`).

**A generic template is included in this repo** at [`/llms.txt`](/llms.txt). Edit it for your project before deploying.

**Format**: Markdown with:
- `# H1` — project/site name
- Blockquote — one-sentence description
- Sections with `## headings` grouping related links
- Each link: `- [Page Title](/path): one-line description`

**In Next.js**: Create `app/llms.txt/route.ts` returning `text/plain; charset=utf-8`. Lets you generate it dynamically from your content.

**In plain Node.js / Express**: Serve it as a static file or a dedicated route:
```js
app.get('/llms.txt', (req, res) => {
  res.type('text/plain').sendFile(path.join(__dirname, 'llms.txt'));
});
```

### `/llms-full.txt` — Optional Full-Content Companion

An increasingly adopted companion file at `/llms-full.txt` containing the full site content flattened into plain Markdown. Useful for AI agents that need complete context (documentation sites, product pages, knowledge bases). Keep it under ~100k tokens. Not required, but high-signal for AEO on content-heavy sites.

---

## `robots.txt` — Crawler Directives

**What it is**: A plain-text file at the domain root that tells web crawlers (Google, Bing, AI bots) which paths they may or may not access.

**Where it lives**: Project root, served at `/robots.txt`.

**A generic template is included in this repo** at [`/robots.txt`](/robots.txt). Customize `Sitemap:` to your actual domain before deploying.

**Key directives**:
- `User-agent: *` — applies to all crawlers
- `Allow: /` — permits access to all paths
- `Disallow: /admin` — blocks a path
- `Sitemap:` — points crawlers to your sitemap

**AI-specific bots** (as of 2026): `GPTBot` (OpenAI), `ClaudeBot` (Anthropic), `PerplexityBot`, `GoogleOther` (Google AI). The included template allows all of these by default. Block them explicitly if your content is not intended for AI training or synthesis.

---

## Structured Data — JSON-LD

**What it is**: Machine-readable metadata embedded in your HTML `<head>` using `<script type="application/ld+json">`. Tells AI engines and search crawlers the *type* and *relationships* of your content.

**Why it matters for AEO**: AI engines use schema.org entities to understand what your page is *about*, not just what words appear on it. A page with `Organization` schema is more likely to be cited as an authoritative source about that org than one without.

**Key schema types** (use what applies to your project):

| Schema | Use case |
|---|---|
| `Organization` | Company/project identity, contact info |
| `Person` | Team members, authors |
| `Article` / `BlogPosting` | Blog posts, news |
| `Service` | Service pages |
| `FAQPage` | FAQ sections — high AEO value, AI engines pull directly |
| `BreadcrumbList` | Navigation hierarchy |
| `WebSite` | Sitelinks searchbox, site identity |
| `SoftwareApplication` | App/tool pages |

**Implementation**: Add per-page, not globally. Each page gets the schema relevant to its content.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "What does this product do?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "It does X, Y, and Z."
    }
  }]
}
</script>
```

**In Next.js**: Inject via `generateMetadata` or a `<JsonLd>` component in your page layout. Can be generated dynamically from CMS data.

---

## Canonical URLs + `sitemap.xml`

**Canonical URLs**: The `<link rel="canonical" href="...">` tag tells crawlers which URL is the authoritative version of a page. Prevents duplicate content penalties when pages are accessible via multiple URLs (e.g., with/without trailing slash, with query params).

**`sitemap.xml`**: An XML index of all crawlable pages with optional metadata (last modified, priority). Submit to Google Search Console and Bing Webmaster Tools.

**In Next.js (App Router)**: Create `app/sitemap.ts` returning a `MetadataRoute.Sitemap` array — generates `/sitemap.xml` automatically. Canonical tags are set via `generateMetadata`.

**In plain Node.js**: Use `sitemap` (npm) to generate and serve the XML, or generate a static file at build time.

---

## OpenGraph + Twitter Card Meta

**What it is**: `<meta>` tags in `<head>` that control how your pages appear when shared on social platforms, in messaging apps, and increasingly in AI-generated summaries.

**Why it matters for AEO**: When structured data is absent or incomplete, AI systems fall back to OG meta for title, description, and image. It's a low-effort, high-return signal.

**Minimum viable set**:
```html
<meta property="og:title" content="Page Title" />
<meta property="og:description" content="One to two sentence summary." />
<meta property="og:image" content="https://yourdomain.com/og-image.png" />
<meta property="og:url" content="https://yourdomain.com/page" />
<meta property="og:type" content="website" />
<meta name="twitter:card" content="summary_large_image" />
```

**In Next.js**: Handled via `generateMetadata` — returns a typed `Metadata` object. No manual tag writing needed.

---

## Semantic HTML

Crawler and AI legibility depends on correct HTML structure. Both SEO and AEO weight this.

- One `<h1>` per page — the page's primary topic
- `<h2>` / `<h3>` for subsections — creates scannable hierarchy for AI summarization
- `<main>`, `<article>`, `<nav>`, `<footer>`, `<aside>` — landmark elements signal content roles
- `<time datetime="...">` — machine-readable dates
- Descriptive `alt` text on images — used by AI vision and accessibility crawlers

This applies equally to Node.js-rendered templates and Next.js React components.

---

## Avoiding JavaScript-Only Rendering

**The problem**: If your content is rendered client-side via JavaScript (standard SPA behavior), many AI crawlers and some search crawlers never see it. They receive an empty HTML shell and index nothing.

**The fix**: Server-side rendering (SSR) or static generation (SSG) — your HTML arrives fully populated.

- **Node.js + Express**: Use server-side templating (Handlebars, EJS, Nunjucks) or a rendering layer
- **React without a framework**: You are likely in a risky SPA configuration for SEO/AEO
- **Next.js**: SSR and SSG are the defaults. Every page is server-rendered unless you explicitly opt into client-only behavior

If your project serves any public-facing pages with content that should be indexed or cited, JavaScript-only rendering is the single highest-impact risk to address.

---

## Next.js — When and Why

This starter is a **Node.js project**. If your project serves public-facing web pages that need to be found, cited, or ranked, consider adding Next.js. It is the most complete SSR/SSG solution for the Node.js ecosystem and provides the best out-of-the-box AEO/SEO infrastructure.

**Next.js earns the recommendation specifically because**:

| Feature | SEO/AEO benefit |
|---|---|
| App Router + `generateMetadata` | Per-page title, description, OG, canonical — typed, colocated with the route |
| Server Components (RSC) | Content is in the HTML by default — no JS required for crawlers |
| `next/image` | Automatic WebP/AVIF conversion, lazy loading, size hints — directly improves LCP |
| `app/sitemap.ts` | Auto-generates `/sitemap.xml` from your route data |
| `app/robots.ts` | Programmatic `robots.txt` generation |
| `app/llms.txt/route.ts` | Trivially serve a dynamic AI discovery file |
| Built-in code splitting | Smaller JS bundles → faster TTI → better Core Web Vitals |
| Vercel deployment | Edge network, automatic CDN, image optimization CDN — all Core Web Vitals positive |

**Next.js is not required if**: your project is a pure API, a CLI tool, a background service, or a server-rendered app using traditional templating that already handles the above concerns.

---

## Core Web Vitals & Performance

Google's Core Web Vitals (LCP, INP, CLS) remain ranking signals in 2026 and correlate with AI Overview inclusion.

- **LCP (Largest Contentful Paint)**: Target < 2.5s. `next/image` and SSG are the most impactful levers.
- **INP (Interaction to Next Paint)**: Replaced FID in 2024. Measures input responsiveness. Heavy JS = high INP.
- **CLS (Cumulative Layout Shift)**: Avoid layout shifts from async content, fonts, or images without dimensions.

**Framer Motion note**: If your project uses Framer Motion for animations, be aware that heavy usage increases JS bundle size and can raise INP. Prefer `motion` variants with `lazy` or dynamic imports, and avoid animating layout-affecting properties (`width`, `height`, `top`, `left`) in favor of `transform` and `opacity`.

---

## AEO Content Strategy

Technical signals matter, but AI engines ultimately cite content that *directly answers questions*. Structural recommendations:

- **Answer-first (BLUF)**: Put the direct answer at the top of any section, before context or caveats. AI systems often quote the first substantive sentence.
- **FAQ sections**: `FAQPage` JSON-LD + an actual FAQ section on key pages is one of the highest-value AEO tactics. AI Overviews pull from FAQ schema frequently.
- **Specific, authoritative content**: Vague content is not cited. Specific claims, data, and named entities are.
- **Internal linking**: Link related pages explicitly. AI crawlers follow link graphs to understand content relationships and authority. Deep, well-linked content clusters outperform isolated pages.
- **Content depth**: A thorough 1,500-word page on one topic outperforms five shallow 300-word pages for AEO citation.

---

## Reference: Starter Prompt

See [`_STARTER-PROMPTS/SEO-AEO-SETUP.md`](/_STARTER-PROMPTS/SEO-AEO-SETUP.md) for a ready-to-use AI IDE prompt that audits your project and auto-generates the recommended SEO/AEO infrastructure above.

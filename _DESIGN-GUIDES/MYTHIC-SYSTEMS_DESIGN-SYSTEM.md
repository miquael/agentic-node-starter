# UI/UX Design Playbook

> A portable design language guide for building premium, dark-mode-first interfaces with glassmorphism, strong typography, and conversion-focused layouts. Use this document as a reference when starting a new project or integrating these design patterns into an existing one. All patterns are framework-agnostic; CSS class names and snippet conventions follow Tailwind CSS.

---

## Design Philosophy

Four principles that govern every decision:

1. **Consistency First** — default to established patterns; deviate only with strategic justification
2. **Premium & Purposeful** — sophisticated palette, motion, and glassmorphism; every effect earns its place
3. **Conversion-Focused** — clear visual hierarchy guides users from discovery through to action
4. **Accessible by Default** — WCAG 2.1 AA contrast, keyboard navigation, reduced-motion support

---

## Typography

A three-font system covering brand identity, editorial headings, and functional UI:

| Font | Role | Rules |
|------|------|-------|
| **Rajdhani** | Wordmark / Logo | `font-weight: 600`, `letter-spacing: 0.05em` |
| **Exo 2** | H1, H2 — editorial headings | `font-weight: 600`, `text-transform: uppercase`, `letter-spacing: 0.05em` |
| **Inter** | H3–H6, body, buttons, UI | `font-weight: 700` (headings), `400–600` (body/UI) |

> **Rule of thumb:** Exo 2 belongs to brand/editorial moments. Inter belongs to functional/data contexts. Never use a display font inside tables, charts, or dense data grids.

### Type Scale

| Element | Size | Notes |
|---------|------|-------|
| Hero H1 | `3xl–7xl` responsive | Animated or gradient text supported |
| Section H2 | `4xl–5xl` | Uppercase, tracked out |
| Component H3–H6 | `xl–2xl` | Sentence case, tighter tracking |
| Body large | `lg–xl` | Supporting copy under headings |
| Body regular | `base` | Default paragraph text |
| Stat / metric | `4xl–5xl` | Bold, display treatment |
| Navigation | `lg` | Medium weight |
| Button label | — | Semibold |
| Logo / wordmark | — | Rajdhani, 600 |

### Named Text Style Classes

Define these as utilities in your CSS layer (Tailwind `@layer utilities` or equivalent):

```css
/* Editorial heading — all-caps, tracked out */
.text-heading-black {
  font-family: 'Exo 2', sans-serif;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

/* Component/section title — sentence case */
.text-component-title {
  font-family: 'Inter', sans-serif;
  font-weight: 600;
  letter-spacing: -0.01em;
}

/* Wordmark / logo lockup */
.text-wordmark {
  font-family: 'Rajdhani', sans-serif;
  font-weight: 600;
  letter-spacing: 0.05em;
}
```

---

## Color Palette

### Dark-Mode Foundation

| Role | Hex | Usage |
|------|-----|-------|
| Primary background | `#0f172a` | Page/app canvas (Slate 900) |
| Secondary background | `#1e293b` | Sections, sidebars (Slate 800) |
| Card background | `#334155` | Cards, panels (Slate 700) |

### Brand Accent Colors

| Name | Hex | Role |
|------|-----|------|
| Cyan 500 | `#06b6d4` | Primary brand, CTAs |
| Cyan 400 | `#22d3ee` | Accents, highlights, hover states |
| Cyan 600 | `#0891b2` | CTA hover (start) |
| Cyan 700 | `#0e7490` | CTA hover (end) |
| Orange 500 | `#f97316` | Energy, innovation |
| Purple 500 | `#a855f7` | Depth, sophistication |
| Pink 500 | `#ec4899` | Warmth, highlights |
| Blue 600 | `#2563eb` | Trust, stability |

### Text Colors

| Token | Hex | Role |
|-------|-----|------|
| White | `#ffffff` | Primary text on dark |
| Slate 300 | `#cbd5e1` | Secondary text |
| Slate 400 | `#94a3b8` | Tertiary text, placeholders |

### Gradient Tokens

Gradients are used for CTAs, section backgrounds, and animated headline text:

| Purpose | Value | Notes |
|---------|-------|-------|
| Primary CTA button | `from-cyan-500 to-cyan-600` → hover `from-cyan-600 to-cyan-700` | Default action |
| Section CTA: content/solution | `from-purple-600 to-pink-600` | Warm-to-vibrant |
| Section CTA: platform/ecosystem | `from-cyan-600 to-purple-600` | Tech-forward |
| Section CTA: newsletter/newsletter | `from-cyan-500 to-blue-600` | Trust-building |
| Global site CTA | `from-cyan-600 via-blue-600 to-purple-600` | Full-spectrum brand |

### Animated Gradient Text

Hero and spotlight headlines can cycle through gradient combinations to create motion:

```css
.gradient-text {
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-size: 200% auto;
}
```

Example gradient set to rotate through:
- **Theme A** — `from-cyan-400 via-cyan-500 to-blue-500`
- **Theme B** — `from-purple-400 via-purple-500 to-pink-500`
- **Theme C** — `from-orange-400 via-pink-500 to-pink-600`
- **Theme D** — `from-cyan-400 via-blue-500 to-purple-500`

---

## Shape System

A custom clip-path system gives UI elements a distinctive "cut-corner" geometry that reinforces the brand's technical, forward-leaning identity. Two complementary shapes create visual pairing between containers and interactive elements.

### Shape Variants

| Variant | Geometry | Typical Use |
|---------|----------|-------------|
| `unique-corners` | Upper-left + lower-right corners cut | Cards, image containers, panels |
| `unique-inverse` | Upper-right + lower-left corners cut | Buttons, badges (inverse of cards) |

The pairing creates visual dialogue between containers and their actions: a card with `unique-corners` contains a button using `unique-inverse`.

### Corner Sizes (responsive)

| Context | Mobile | Tablet | Desktop |
|---------|--------|--------|---------|
| Cards / containers | 25px | 35px | 50px |
| Buttons / badges | 12px | 16px | 20px |

### CSS Implementation

```css
/* Cards */
.clip-unique-corners    { clip-path: polygon(25px 0%, 100% 0%, 100% calc(100% - 25px), calc(100% - 25px) 100%, 0% 100%, 0% 25px); }
.clip-unique-corners-md { clip-path: polygon(35px 0%, 100% 0%, 100% calc(100% - 35px), calc(100% - 35px) 100%, 0% 100%, 0% 35px); }
.clip-unique-corners-lg { clip-path: polygon(50px 0%, 100% 0%, 100% calc(100% - 50px), calc(100% - 50px) 100%, 0% 100%, 0% 50px); }

/* Buttons (inverse geometry) */
.clip-unique-inverse    { clip-path: polygon(0% 0%, calc(100% - 12px) 0%, 100% 12px, 100% 100%, 12px 100%, 0% calc(100% - 12px)); }
.clip-unique-inverse-md { clip-path: polygon(0% 0%, calc(100% - 16px) 0%, 100% 16px, 100% 100%, 16px 100%, 0% calc(100% - 16px)); }
.clip-unique-inverse-lg { clip-path: polygon(0% 0%, calc(100% - 20px) 0%, 100% 20px, 100% 100%, 20px 100%, 0% calc(100% - 20px)); }
```

Apply responsively: `clip-unique-inverse md:clip-unique-inverse-md lg:clip-unique-inverse-lg`

---

## Buttons

### Primary (CTA)

Solid white on gradient or dark background, clipped inverse geometry:

```
bg-white hover:bg-gray-100 text-blue-600
clip-unique-inverse md:clip-unique-inverse-md lg:clip-unique-inverse-lg
font-sans font-semibold text-lg px-8 py-4
transition-all duration-200 transform hover:scale-105
```

### Secondary (Ghost / Outline)

Transparent with white border, fills on hover, glassmorphism applied:

```
border-2 border-white hover:bg-white hover:text-cyan-400 text-white
clip-unique-inverse md:clip-unique-inverse-md lg:clip-unique-inverse-lg
font-sans font-semibold text-lg px-8 py-4 glass-medium
```

### Tertiary / Text

Text-only with underline animation, no background. Use for de-emphasized or inline actions.

### Icon Conventions in Buttons

- Pair with a directional or contextual icon (right side of label)
- Arrow icons nudge on hover: `group-hover:translate-x-1 transition-transform`
- Calendar/schedule icons pair with booking/scheduling CTAs
- Icon size: match font size — `w-5 h-5` for `text-lg` buttons

---

## Glassmorphism

Glass effects create a sense of depth and layering on dark backgrounds. Applied via CSS utility classes, never inline styles, so the system can be toggled for low-end devices.

### Core Classes

| Class | Blur | BG Opacity | Use |
|-------|------|------------|-----|
| `.glass-subtle` | 4px | 10% white | Buttons, light overlays |
| `.glass-medium` | 8px | 15% white | Cards, containers |
| `.glass-strong` | 12px | 20% white | Prominent elements, modals |
| `.glass-dark-subtle` | 4px | 10% black | Light-background contexts |
| `.glass-dark-medium` | 12px | 30% black | Sticky header / nav bar |
| `.glass-cyan` | 4px | Cyan-tinted | Primary CTA buttons on dark bg |

### CSS Implementation

```css
.glass-subtle {
  backdrop-filter: blur(4px);
  background-color: rgba(255, 255, 255, 0.10);
  border: 1px solid rgba(255, 255, 255, 0.12);
}

.glass-medium {
  backdrop-filter: blur(8px);
  background-color: rgba(255, 255, 255, 0.15);
  border: 1px solid rgba(255, 255, 255, 0.15);
}

.glass-strong {
  backdrop-filter: blur(12px);
  background-color: rgba(255, 255, 255, 0.20);
  border: 1px solid rgba(255, 255, 255, 0.18);
}

.glass-dark-medium {
  backdrop-filter: blur(12px);
  background-color: rgba(0, 0, 0, 0.30);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
}

.glass-cyan {
  backdrop-filter: blur(4px);
  background-color: rgba(6, 182, 212, 0.15);
  border: 1px solid rgba(6, 182, 212, 0.25);
}
```

### Responsive Blur Scaling

Reduce blur on lower-capability devices:

| Device tier | Blur |
|------------|------|
| Mobile (<640px) | 2px |
| Tablet (641–1024px) | 3–10px (varies by class) |
| Desktop (>1024px) | 4–12px (full values) |

### Performance Degradation Classes

Add these to `<body>` via JS feature detection — allow CSS to automatically scale back effects:

```css
.low-end-device .glass-medium,
.low-fps .glass-medium { backdrop-filter: blur(4px); }

.minimal-glass .glass-medium,
.minimal-glass .glass-strong { backdrop-filter: none; background-color: rgba(30, 41, 59, 0.95); }
```

Always preserve sticky header glass at full quality — it defines the brand presence.

### Focus States

Glass elements use a cyan focus ring:

```css
.glass-medium:focus,
.glass-subtle:focus {
  outline: 2px solid rgba(6, 182, 212, 0.5);
  outline-offset: 2px;
}
```

---

## Icon System

A semantic icon system pairs each context with the appropriate visual weight and container geometry.

### Semantic Variants

| Variant | Use Case | Shape | Default Size | Glow |
|---------|----------|-------|-------------|------|
| `display` | Hero / landing "What We Do" | Circle | ~112px (w-28) | Yes — heavy |
| `section-hero` | Page headers, key stats | Circle | ~80px (w-20) | Yes |
| `card-icon` | Standard feature cards | Square | ~64px (w-16) | Yes |
| `process-step` | Numbered steps in a linear flow | Square | ~48px (w-12) | No |
| `process-circle` | Circular / "How It Works" flows | Circle | ~80px (w-20) | No |
| `subtle-card` | Dense grids, secondary content | Square | ~48px (w-12) | No |
| `step-circle` | Numbered steps with circle badge | Circle | ~64px (w-16) | No |
| `icon-only` | Inline, no container boundary | Square | ~48px | No |

### Icon Color Palette

Use one semantic color per icon per context — do not mix within a single card:

`cyan` (primary) · `purple` · `emerald` · `amber` · `amber-dim` · `blue` · `orange` · `white` · `indigo` · `green` · `red` · `pink` · `yellow` · `gray`

### Glow Implementation

```css
.icon-glow-cyan {
  filter: drop-shadow(0 0 8px rgba(6, 182, 212, 0.6));
}
.icon-glow-purple {
  filter: drop-shadow(0 0 8px rgba(168, 85, 247, 0.6));
}
```

---

## Cards & Panels

### Feature Card

```
glass-medium clip-unique-corners md:clip-unique-corners-md lg:clip-unique-corners-lg
p-6 md:p-8
border border-white/10 hover:border-cyan-500/30
transition-all duration-300 hover:-translate-y-1
```

Structure:
1. Icon (top, `card-icon` variant)
2. Heading (`text-component-title`)
3. Body copy (`text-slate-300`)
4. Optional: CTA link or stat

### Stat / Metric Card

```
glass-medium clip-unique-corners
p-6 text-center
```

Structure:
1. Large number (`text-4xl font-bold text-white` or gradient text)
2. Label (`text-slate-400 text-sm uppercase tracking-widest`)

### Panel / Section Block

Full-width section backgrounds alternate between `bg-slate-900` and `bg-slate-800` to create rhythm. Avoid more than two adjacent sections of the same tone.

---

## Header / Navigation

### Sticky Header

```css
/* Base */
position: sticky; top: 0; z-index: 50;
/* Apply glass-dark-medium */
backdrop-filter: blur(12px);
background-color: rgba(0, 0, 0, 0.30);
border-bottom: 1px solid rgba(255, 255, 255, 0.08);
```

Content layout: `flex items-center justify-between` — logo left, nav center/right, primary CTA button rightmost.

Nav links: `text-slate-300 hover:text-white transition-colors duration-200`

Active/current page: `text-white` or `text-cyan-400`

---

## Layout & Spacing

### Container

```css
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 1.5rem; /* px-6 */
}
```

### Breakpoints (Tailwind default)

| Token | Width | Behavior |
|-------|-------|----------|
| `sm` | 640px | Large mobile — single column shifts |
| `md` | 768px | Tablet — 2-col layouts activate |
| `lg` | 1024px | Desktop — multi-col, full nav |
| `xl` | 1280px | Large desktop |
| `2xl` | 1536px | Wide screen |

### Spacing Scale

Base unit: **8px**. Common values: 4 · 8 · 12 · 16 · 20 · 24 · 32 · 48 · 64 · 80px.

Section vertical rhythm: `py-20` (standard), `py-16` (compact).

### Grid Patterns

| Pattern | Classes |
|---------|---------|
| Feature / service grid | `grid grid-cols-1 md:grid-cols-3 gap-8` |
| Two-column hero | `grid grid-cols-1 lg:grid-cols-5 gap-12` (60/40 split) |
| Two-column content | `grid grid-cols-1 md:grid-cols-2 gap-10` |
| Four-column stats | `grid grid-cols-2 md:grid-cols-4 gap-6` |

---

## Motion & Animation

### Principles

- Motion communicates state changes, not decoration
- All animations respect `prefers-reduced-motion: reduce`
- Keep durations short: 200ms for micro-interactions, 300–500ms for transitions, ≥1s only for ambient loops

### Standard Transitions

| Interaction | Classes |
|------------|---------|
| Hover (general) | `transition-all duration-200` |
| Button scale | `hover:scale-105` |
| Card lift | `hover:-translate-y-1 transition-transform duration-300` |
| Arrow nudge | `group-hover:translate-x-1 transition-transform` |
| Glass state change | `transition: background-color 0.2s ease, border-color 0.2s ease` |
| Active press | `transform: scale(0.98)` |

### Scroll Animations

```css
@keyframes fade-in-up {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
.animate-fade-in-up {
  animation: fade-in-up 500ms ease-out both;
}
```

### Infinite Scroll Carousel (logos, marquee)

```css
@keyframes infinite-scroll {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}
.animate-infinite-scroll {
  animation: infinite-scroll 60s linear infinite;
}
.animate-infinite-scroll:hover { animation-play-state: paused; }
```

### Headline Word Rotation

Cycle through words/phrases with a crossfade:

```css
@keyframes fade-crossfade {
  0%, 15%  { opacity: 1; }
  25%, 90% { opacity: 0; }
  100%     { opacity: 1; }
}
```
Switch every ~5000ms. Pause on `prefers-reduced-motion`.

### Reduced Motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Accessibility

| Category | Requirement |
|----------|-------------|
| **Contrast** | Text ≥4.5:1 (normal), ≥3:1 (large text/UI) — WCAG 2.1 AA |
| **Focus** | Visible outline on all interactive elements; cyan ring on glass elements |
| **Keyboard** | Full tab order; dropdowns keyboard-navigable; skip links on long pages |
| **Semantic HTML** | Proper H1→H6 hierarchy; `alt` on all images; ARIA labels where visual context is absent |
| **Color independence** | State and status conveyed by shape/label, not color alone |
| **Heading hierarchy** | Never skip levels; H1 once per page; H2 for sections; H3+ for components |
| **Motion** | All animations honor `prefers-reduced-motion`; no autoplay with no override |

---

## Section & Page Architecture

### Universal Page Structure

```
Header (sticky nav + logo + primary CTA)
Hero (headline + subhead + dual CTAs + visual element)
  └── Primary CTA: high-intent action (schedule, start, etc.)
  └── Secondary CTA: lower-commitment (learn more, explore)
Feature / Value sections (3-col grids, alternating tone)
Social proof (testimonials, metrics, logos)
Newsletter / lead capture
Global CTA (gradient banner → high-intent action)
Footer (links + contact + social)
```

### CTA Gradient by Context

| Page / Section Type | Gradient | Signal |
|---------------------|----------|--------|
| Content / article / guide | `from-purple-600 to-pink-600` | Depth, editorial |
| Solution / product | `from-purple-600 to-pink-600` | Authority |
| Platform / ecosystem | `from-cyan-600 to-purple-600` | Technology |
| Newsletter | `from-cyan-500 to-blue-600` | Trust |
| Global site CTA | `from-cyan-600 via-blue-600 to-purple-600` | Full brand |

### Information Hierarchy for Feature Sections

1. Section label (`text-sm uppercase text-cyan-400 tracking-widest`)
2. Section heading H2 (`text-heading-black`)
3. Supporting paragraph (`text-slate-300 text-lg max-w-2xl`)
4. Grid of cards/features below

---

## Design Checklist for New Screens

- [ ] Identify section/page type → select correct CTA gradient
- [ ] Apply `text-heading-black` to H1/H2, `text-component-title` to H3–H6
- [ ] Use `clip-unique-inverse` on buttons, `clip-unique-corners` on cards
- [ ] Use semantic icon variants (match display weight to context)
- [ ] Alternate section backgrounds (`slate-900` / `slate-800`) for rhythm
- [ ] Verify color contrast meets WCAG 2.1 AA
- [ ] Test hover, focus, and active states on all interactive elements
- [ ] Confirm layout at all breakpoints (mobile → desktop)
- [ ] Validate reduced-motion — no motion should be required to use any feature
- [ ] Ensure heading hierarchy is correct and H1 appears once

---

## When to Break the Rules

**Acceptable deviations:**
- New product lines that warrant a distinct visual sub-identity
- A/B test variants with explicit scoping
- Accessibility improvements that require contrast or spacing overrides
- Data-dense components that require Inter over display fonts

**Not acceptable:**
- Personal aesthetic preference without strategic rationale
- One-off designs that create inconsistency without encapsulation
- Overriding the font system without a scoped class
- Glassmorphism in contexts without a dark or blurred background — always provide an opaque fallback

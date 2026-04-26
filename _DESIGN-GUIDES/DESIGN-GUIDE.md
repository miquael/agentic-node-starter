# Design Guide — Node.js Web Applications (2026)

> A framework-agnostic design reference for building modern Node.js web interfaces. Use this as a starting point — adapt it to your project's specific needs. Formatted for AI agent consumption.

Reference: see `DESIGN-GUIDE-DEMO.png` for a simple example of a Node.js front page designed using these principles.

---

## Design Philosophy

1. **Clarity over decoration** — Every visual element should serve a function. Remove what doesn't communicate.
2. **Performance-first** — Design decisions that require heavy JS or large assets should be justified. Prefer CSS-native solutions.
3. **Accessible by default** — WCAG 2.1 AA is the minimum. Contrast, keyboard navigation, and screen reader support are non-negotiable.
4. **Dark mode ready** — Use CSS custom properties for all color values. Support both light and dark modes via `prefers-color-scheme`.
5. **Mobile-first** — Design and build for small screens first, then scale up.

---

## Typography

### Font Stack (System)
```css
--font-sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
--font-mono: 'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;
```

### Type Scale
| Token | Size | Use |
|---|---|---|
| `--text-xs` | 12px | Labels, captions |
| `--text-sm` | 14px | Secondary text, metadata |
| `--text-base` | 16px | Body text (default) |
| `--text-lg` | 18px | Subheadings |
| `--text-xl` | 20px | Section headings |
| `--text-2xl` | 24px | Page headings |
| `--text-3xl` | 30px+ | Display / hero |

### Principles
- Line height: 1.5 for body, 1.2 for headings
- Max line width: 65–75 characters (`65ch`)
- Avoid more than 2 typefaces per project

---

## Color System

### CSS Custom Properties Pattern
```css
:root {
  /* Neutral */
  --color-bg: #ffffff;
  --color-surface: #f5f5f5;
  --color-border: #e0e0e0;
  --color-text: #111111;
  --color-text-muted: #6b6b6b;

  /* Brand */
  --color-primary: #3b82f6;
  --color-primary-hover: #2563eb;

  /* State */
  --color-success: #22c55e;
  --color-warning: #f59e0b;
  --color-error: #ef4444;
  --color-info: #06b6d4;
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0f0f0f;
    --color-surface: #1a1a1a;
    --color-border: #2a2a2a;
    --color-text: #f0f0f0;
    --color-text-muted: #9a9a9a;
  }
}
```

### Principles
- Never hardcode hex values in component styles — always use tokens
- Ensure 4.5:1 contrast ratio for all body text (WCAG AA)
- Use semantic color tokens (`--color-error`) not value tokens (`--color-red-500`) in components

---

## Spacing & Layout

### Spacing Scale (4px base unit)
```css
--space-1: 4px;
--space-2: 8px;
--space-3: 12px;
--space-4: 16px;
--space-6: 24px;
--space-8: 32px;
--space-12: 48px;
--space-16: 64px;
```

### Layout Patterns
- **Page max-width**: 1200–1440px with centered container
- **Content max-width**: 720–800px for text-heavy pages
- **Grid**: CSS Grid for two-dimensional layouts; Flexbox for one-dimensional
- **Sidebar layout**: `grid-template-columns: 240px 1fr` (fixed sidebar, fluid content)

---

## Components

### Cards
- Background: `--color-surface`
- Border: `1px solid var(--color-border)`
- Border radius: 8px
- Padding: `--space-6` (24px)
- Box shadow: subtle — `0 1px 3px rgba(0,0,0,0.08)`

### Buttons
| Variant | Use |
|---|---|
| Primary | Main CTA, one per view |
| Secondary | Secondary actions |
| Ghost | Tertiary / low-emphasis actions |
| Destructive | Delete / irreversible actions |

- Minimum touch target: 44×44px
- Padding: `--space-2` vertical, `--space-4` horizontal
- Border radius: 6px

### Forms
- Label always visible (never placeholder-only)
- Error messages below the field, in `--color-error`
- Required fields marked explicitly
- Input height: 40px minimum

### Navigation
- Active state must use `aria-current="page"`
- Mobile: hamburger or bottom nav bar
- Include a skip-to-content link for keyboard users

---

## State Patterns (API / Data-Driven UIs)

Essential for Node.js API-driven interfaces.

| State | Visual Treatment |
|---|---|
| **Loading** | Skeleton loaders (not spinners for content areas) |
| **Error** | Inline message + retry action |
| **Empty** | Icon/illustration + explanation + primary CTA |
| **Success** | Toast or inline confirmation (auto-dismiss after 4s) |
| **Offline** | Persistent banner, not a modal |

---

## Motion & Animation

- Use CSS transitions, not JS animation libraries by default
- Avoid `transition: all` — be explicit: `transition: opacity 150ms ease, transform 150ms ease`
- Respect reduced motion preferences:
```css
@media (prefers-reduced-motion: reduce) {
  *, ::before, ::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```
- Typical durations: enter 150–200ms, exit 100–150ms, page transitions 200–300ms

---

## Accessibility Checklist

- [ ] All interactive elements are keyboard-reachable
- [ ] Focus styles are visible (`outline` not removed without replacement)
- [ ] Images have `alt` text (empty `alt=""` for decorative images)
- [ ] Form inputs have associated `<label>` elements
- [ ] Color is not the only means of conveying information
- [ ] Dynamic content updates are announced via `aria-live`
- [ ] Page has a single `<h1>`, with logical heading order

---

## CSS Approach

- **CSS custom properties** for all design tokens
- **No CSS-in-JS** by default (adds bundle weight, complicates SSR)
- **BEM or flat utility classes** — pick one convention and be consistent
- No `!important` except in a dedicated reset/overrides layer
- Colocate component styles near their components

### Suggested File Structure
```
styles/
├── tokens.css        # All CSS custom properties
├── reset.css         # Minimal reset (box-sizing, margin: 0)
├── typography.css    # Base type styles
├── layout.css        # Page layout, grid, container
└── components/       # Per-component stylesheets
```

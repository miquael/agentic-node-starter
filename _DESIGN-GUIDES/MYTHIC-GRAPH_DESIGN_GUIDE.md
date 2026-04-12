# Design Guide — MYTHIC-GRAPH Aesthetic System

A portable reference for adopting the visual language, layout patterns, and component conventions of the MYTHIC-GRAPH viewer into any new application. Each section leads with the design principle, then the specific implementation.

---

## Purpose

This guide distills a dark, data-dense, technical UI aesthetic into adoptable patterns. The visual language suits applications that deal with structured data, file systems, knowledge graphs, developer tooling, or any context where density and clarity matter more than decoration. The look is precise, layered, and purposeful — a serious tool that doesn't hide its technical nature.

---

## Design Philosophy

Four principles drive every decision in this system:

1. **Dark-first.** The UI is designed in dark mode as the primary and only theme. Light mode is not a fallback — the surface hierarchy is built entirely on dark gray layers.
2. **Layered surfaces.** Depth is communicated by stacking slightly lighter gray surfaces on a dark base, not by shadows or gradients. Each layer has a defined role.
3. **Chromatic role-coding.** Colors are reserved for function, not decoration. Each action type gets its own color family (emerald = sync, purple = tools, blue = navigation/info). Warm colors (yellow, red) signal warnings and destructive actions only.
4. **Minimal chrome.** Borders, text, and icons do the structural work. There are no drop shadows on interactive elements, no rounded corners above `0.5rem`, no gradients. The canvas and data are the focus.

---

## Quick Start

Minimum setup to establish this aesthetic in a new React + Tailwind project:

**1. Install dependencies**
```bash
pnpm add tailwindcss clsx class-variance-authority lucide-react
pnpm add @fontsource-variable/inter @fontsource-variable/exo-2
```

**2. Set dark mode at the HTML root** (`index.html`)
```html
<html lang="en" class="dark">
  <body class="bg-gray-900 text-white">
```

**3. Import fonts** (entry point, e.g. `main.tsx`)
```ts
import '@fontsource-variable/inter'
import '@fontsource-variable/exo-2'
```

**4. Add CSS variables** to your global stylesheet (see §Design Tokens below)

**5. Extend Tailwind** with semantic color tokens and font families (see §Foundation Stack below)

**6. Set body defaults**
```css
body {
  font-family: 'Inter Variable', Inter, sans-serif;
  background-color: hsl(var(--background));
  color: hsl(var(--foreground));
}
```

That's enough to get the surface, type hierarchy, and color system running.

---

## Foundation Stack

| Layer | Technology | Role |
|---|---|---|
| Framework | React 18+ / TypeScript | Component model |
| Build | Vite | Dev server and bundler |
| Styling | Tailwind CSS 3.4+ | Utility classes |
| Color system | CSS custom properties (HSL) | Semantic tokens, theme switching |
| Component variants | `class-variance-authority` (CVA) | Typed variant APIs |
| Class merging | `clsx` | Conditional class composition |
| Icons | `lucide-react` | SVG icon library |
| Fonts | `@fontsource-variable/*` | Self-hosted variable fonts, no CDN |

**`cn()` utility — use everywhere class composition is needed:**
```ts
import { type ClassValue, clsx } from 'clsx'

export function cn(...inputs: ClassValue[]) {
  return clsx(inputs)
}
```

---

## Design Tokens

Define HSL-based CSS variables in your global stylesheet. Tailwind then references them as `hsl(var(--token))`. This decouples color values from their semantic roles — you can retheme by swapping variable values, not class names.

```css
@layer base {
  :root {
    /* Light mode values — defined but not used (dark-first app) */
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
    --secondary: 210 40% 96%;
    --secondary-foreground: 222.2 47.4% 11.2%;
    --muted: 210 40% 96%;
    --muted-foreground: 215.4 16.3% 46.9%;
    --accent: 210 40% 96%;
    --accent-foreground: 222.2 47.4% 11.2%;
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;
    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
    --radius: 0.5rem;
  }

  .dark {
    /* Active theme values */
    --background: 222.2 84% 4.9%;      /* gray-900 equivalent */
    --foreground: 210 40% 98%;          /* near-white */
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 11.2%;
    --secondary: 217.2 32.6% 17.5%;    /* gray-800 equivalent */
    --secondary-foreground: 210 40% 98%;
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 212.7 26.8% 83.9%;
  }
}
```

**Wire into Tailwind** (`tailwind.config.js`):
```js
export default {
  darkMode: ['class'],
  content: ['./src/**/*.{ts,tsx}'],
  theme: {
    extend: {
      colors: {
        border:      'hsl(var(--border))',
        input:       'hsl(var(--input))',
        ring:        'hsl(var(--ring))',
        background:  'hsl(var(--background))',
        foreground:  'hsl(var(--foreground))',
        primary:     { DEFAULT: 'hsl(var(--primary))', foreground: 'hsl(var(--primary-foreground))' },
        secondary:   { DEFAULT: 'hsl(var(--secondary))', foreground: 'hsl(var(--secondary-foreground))' },
        destructive: { DEFAULT: 'hsl(var(--destructive))', foreground: 'hsl(var(--destructive-foreground))' },
        muted:       { DEFAULT: 'hsl(var(--muted))', foreground: 'hsl(var(--muted-foreground))' },
        accent:      { DEFAULT: 'hsl(var(--accent))', foreground: 'hsl(var(--accent-foreground))' },
        card:        { DEFAULT: 'hsl(var(--card))', foreground: 'hsl(var(--card-foreground))' },
      },
      borderRadius: {
        lg: 'var(--radius)',
        md: 'calc(var(--radius) - 2px)',
        sm: 'calc(var(--radius) - 4px)',
      },
      fontFamily: {
        exo:   ['"Exo 2 Variable"', '"Exo 2"', 'sans-serif'],
        inter: ['Inter Variable', 'Inter', 'sans-serif'],
      },
    },
  },
}
```

> **Why HSL + CSS variables?** HSL values are human-readable and easy to adjust. CSS variables allow the `.dark` class to swap the entire theme by overriding the variable layer — no Tailwind class duplication required.

---

## Typography

Two fonts, two roles. They never overlap in purpose.

| Role | Font | Tailwind | Style |
|---|---|---|---|
| App title / brand identity | **Exo 2** | `font-exo` | `text-2xl font-bold uppercase tracking-[0.1em]` |
| Panel / section headings | **Inter** | `font-inter` | `text-sm font-semibold uppercase tracking-wider` |
| Body / UI labels | **Inter** | `font-inter` (body default) | Regular or medium weight |
| Metadata / captions | **Inter** | — | `text-xs text-gray-400` or `text-[10px]` |
| Sub-brand / system label | **Inter** | — | `text-[10px] font-medium text-gray-300 uppercase tracking-wider` |

**Exo 2** is a geometric sans-serif with a sci-fi/technical character — use it exclusively for the topmost identity element (the app's name). It should appear once per view, large, uppercase, widely tracked.

**Inter** handles everything else. Set it as the body default and never override it except for the brand title.

**Key tracking values:**
- Brand title: `tracking-[0.1em]` — very wide, intentional
- Section headings: `tracking-wider` (Tailwind built-in)
- Sub-labels: `tracking-wider` at `text-[10px]`
- Body: default tracking

---

## Color System

### Structural surface hierarchy (dark mode)

Surfaces are always concrete Tailwind gray classes, not semantic tokens. The layering is what creates visual depth.

| Layer | Class | Role |
|---|---|---|
| App base | `bg-gray-900` | Root body, main container, canvas background |
| Elevated surface | `bg-gray-800` | Sub-header bar, panel header strips, stat cells |
| Panel / overlay | `bg-gray-900/90` + `backdrop-blur-sm` | Floating sidebars over a canvas or background |
| Inset / sunken | `bg-gray-900` inside `bg-gray-800` card | Data cells, code blocks, path displays |
| Borders | `border-gray-700` | All dividers, panel edges, card borders |

Move one step lighter (gray-900 → gray-800) to elevate. Move back to gray-900 to create a sunken/inset effect inside an elevated surface. Never skip steps.

### Text hierarchy

| Role | Class |
|---|---|
| Primary content | `text-white` or `text-gray-200` |
| Secondary labels | `text-gray-300` |
| Muted / metadata | `text-gray-400` |
| Disabled / separators | `text-gray-500` / `text-gray-600` |

### Chromatic accent triplet

This is the core color pattern for action buttons and status indicators. Every chromatic element uses the same three-value triplet from the same color family:

```
bg-{color}-900/50       ← dark, semi-transparent background
border border-{color}-700/50  ← subtly colored border
text-{color}-200        ← light, readable text
hover:bg-{color}-800    ← slightly lighter on hover
```

| Function | Color family | Use case |
|---|---|---|
| Sync / success / confirm | `emerald` | Data sync, save, publish |
| Tools / settings / config | `purple` | Tooling, configuration panels |
| Navigation / info / primary action | `blue` | Current selection, primary CTAs, info panels |
| Warning / truncation / caution | `yellow` | Non-blocking warnings (`text-yellow-500` not `yellow-200`) |
| Destructive / danger | `red` | Delete, remove, irreversible actions |

The `900/50` background makes the button feel contextual and integrated, not loud. The `200` text is light enough to read clearly against it. This pattern scales to any Tailwind color family.

**Active / selected state:** `text-blue-400` — used for the current breadcrumb segment, selected graph nodes, and active panel titles.

---

## App Shell Layout

The overall shell is a fixed-height, flex-column container — no page scrolling. Content regions manage their own overflow internally.

```
<html class="dark">
  <body class="bg-gray-900 text-white font-inter h-screen">
    <div class="h-screen flex flex-col overflow-hidden">
      <header>          ← brand header, flex-shrink-0, always visible
      <nav>             ← accessory/breadcrumb bar, h-10, flex-shrink-0
      <main class="flex-1 overflow-hidden">   ← fills remaining space
        <div class="relative w-full h-full">  ← positioning context
          <canvas />                          ← fills absolute inset-0, z-0
          <Sidebar side="left" />             ← absolute, z-20
          <Sidebar side="right" />            ← absolute, z-20
```

**Why overlay sidebars?** When the central content is a canvas (3D, map, diagram), pushing layout with sidebars wastes the canvas area and creates layout shift on open/close. Overlay panels float above the canvas with semi-transparent backgrounds, letting the content show through.

**Z-index discipline:**
- `z-0` — canvas / background layer
- `z-20` — sidebars and floating panels
- `z-50` — header (always on top)

---

## Header

The brand header is the topmost element. It never scrolls away. It establishes identity on the left and provides global action controls on the right.

### Structure

```
[Left: identity block]                    [Right: action buttons]
  BRAND NAME (Exo 2, uppercase, tracked)    [SYNC ARCHIVE] [TOOLS] [SCANNER]
  System label · descriptor
```

### Identity block (left)

Two lines, stacked:
- **Line 1:** App title in Exo 2, large, uppercase, wide tracking. Optionally followed by an inline alert badge (see §Alert Patterns).
- **Line 2:** Sub-brand context in Inter — a small-caps system label (`text-[10px] uppercase tracking-wider text-gray-300`) followed by a descriptor (`text-xs text-gray-500`). This grounds the app in its broader system context.

```tsx
<div className="flex flex-col">
  <div className="flex items-center gap-4">
    <h1 className="text-2xl font-bold tracking-[0.1em] text-white font-exo uppercase">
      APP NAME
    </h1>
    {/* optional inline alert — see §Alert Patterns */}
  </div>
  <div className="flex items-center gap-2 mt-1 font-inter">
    <span className="text-[10px] font-medium text-gray-300 uppercase tracking-wider whitespace-nowrap">
      System label:
    </span>
    <span className="text-xs text-gray-500 whitespace-nowrap">
      brief descriptor
    </span>
  </div>
</div>
```

### Action buttons (right)

Each button uses the chromatic triplet pattern directly — not the generic `<Button>` component. This allows per-button color identity while sharing the same structural shape.

```tsx
<div className="flex items-center gap-2">
  <button className="flex items-center gap-2 bg-emerald-900/50 hover:bg-emerald-800 border border-emerald-700/50 text-emerald-200 px-4 py-2 rounded text-sm font-medium transition-colors">
    <RefreshCcw size={16} /> SYNC
  </button>
  <button className="flex items-center gap-2 bg-purple-900/50 hover:bg-purple-800 border border-purple-700/50 text-purple-200 px-4 py-2 rounded text-sm font-medium transition-colors">
    <Wrench size={16} /> TOOLS
  </button>
  <button className="flex items-center gap-2 bg-blue-900/50 hover:bg-blue-800 border border-blue-700/50 text-blue-200 px-4 py-2 rounded text-sm font-medium transition-colors">
    <Settings size={16} /> CONFIG
  </button>
</div>
```

**Header container:**
```tsx
<header className="border-b border-gray-700 py-4 px-6 flex-shrink-0 bg-gray-900 flex justify-between items-center z-50 relative">
```

---

## Breadcrumb / Accessory Bar

A slim horizontal bar directly below the header. Height is fixed at `h-10`. Background is `bg-gray-800` — one step lighter than the header, creating a subtle depth step.

**Purpose:** Shows the current navigation path as a clickable trail. Works for any hierarchical structure (file paths, graph nodes, settings categories, etc.).

```tsx
<nav className="h-10 bg-gray-800 border-b border-gray-700 flex items-center px-6 overflow-hidden">
  <div className="flex items-center text-sm gap-1 text-gray-400 overflow-x-auto whitespace-nowrap scrollbar-hide">

    {/* Root — always present, always clickable */}
    <button onClick={navigateToRoot} className="hover:text-white transition-colors cursor-pointer">
      ROOT
    </button>

    {/* Intermediate segments */}
    <ChevronRight size={14} className="text-gray-600" />
    <button onClick={navigateToSegment} className="hover:text-white transition-colors cursor-pointer">
      segment
    </button>

    {/* Active / current segment — colored, not interactive */}
    <ChevronRight size={14} className="text-gray-600" />
    <span className="text-blue-400 font-medium cursor-default">
      current-location
    </span>

  </div>
</nav>
```

**Key conventions:**
- Inactive segments: `text-gray-400 hover:text-white` — subtle, clearly clickable
- Separator chevrons: `text-gray-600` — dimmer than the text, structural not content
- Active segment: `text-blue-400 font-medium` — no hover, `cursor-default`
- The bar scrolls horizontally (`overflow-x-auto`) when paths are long; hide the scrollbar with `scrollbar-hide`

---

## Panels / Sidebars

Floating overlay panels that slide in/out without affecting layout. Used for secondary content: navigation trees, controls, detail views, staging areas.

### Behavior

- Positioned `absolute`, `inset-y-0`, on the `left-0` or `right-0` edge
- Width: `w-80` (320px) — consistent across all panels
- Open/close via CSS `translate-x` transition — `duration-300 ease-in-out`
- `pointer-events-none` on the container; `pointer-events-auto` on the panel and toggle button only (so the canvas remains interactive beneath)

### Toggle tab

A small tab sits flush against the panel edge, facing inward. It uses `bg-gray-800 border border-gray-700 text-gray-400 hover:text-white hover:bg-gray-700`. The chevron direction indicates collapse/expand:
- Left panel open → `ChevronLeft` (click to collapse left)
- Left panel closed → `ChevronRight` (click to expand right)

### Panel anatomy

```tsx
<div className="bg-gray-900/90 backdrop-blur-sm border-r border-gray-700 w-80 h-full flex flex-col">

  {/* Header strip */}
  <div className="p-4 border-b border-gray-700 flex justify-between items-center bg-gray-800/80">
    <h2 className="text-sm font-semibold text-gray-200 uppercase tracking-wider">
      Panel Title
    </h2>
    {/* Optional: panel-level action, e.g. clear button */}
  </div>

  {/* Scrollable content area */}
  <div className="flex-1 overflow-y-auto p-4 space-y-6">
    {/* Cards, sections, lists */}
  </div>

  {/* Optional: fixed footer action */}
  <div className="p-3 bg-gray-900 border-t border-gray-700 mt-auto">
    <button className="w-full ...">Action</button>
  </div>

</div>
```

**Key details:**
- `bg-gray-900/90 backdrop-blur-sm` — semi-transparent so the canvas shows through
- `bg-gray-800/80` on the header strip — lighter, slightly transparent, creates depth against the panel body
- Panel title: `text-sm font-semibold text-gray-200 uppercase tracking-wider` — matches section heading convention
- Content area: `space-y-6` between card groups; `p-4` padding

---

## Component Primitives

### Button (CVA)

A typed, variant-based button for standard UI controls. Uses semantic tokens from the CSS variable system.

```tsx
const buttonVariants = cva(
  "inline-flex items-center justify-center rounded-md text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50",
  {
    variants: {
      variant: {
        default:     "bg-primary text-primary-foreground hover:bg-primary/90",
        destructive: "bg-destructive text-destructive-foreground hover:bg-destructive/90",
        outline:     "border border-input bg-background hover:bg-accent hover:text-accent-foreground",
        secondary:   "bg-secondary text-secondary-foreground hover:bg-secondary/80",
        ghost:       "hover:bg-accent hover:text-accent-foreground",
        link:        "text-primary underline-offset-4 hover:underline",
      },
      size: {
        default: "h-10 px-4 py-2",
        sm:      "h-9 rounded-md px-3",
        lg:      "h-11 rounded-md px-8",
        icon:    "h-10 w-10",
      },
    },
    defaultVariants: { variant: "default", size: "default" },
  }
)
```

> Note: Header action buttons with color identity (SYNC, TOOLS, etc.) **bypass** this component and use the chromatic triplet pattern directly. Use `<Button>` for standard controls inside panels and modals.

---

### Card

The base container for grouped information. Used throughout panels for data blocks, info sections, and staging lists.

```tsx
// Base — rounded-lg border bg-card shadow-sm
<Card className="bg-gray-800 border-gray-700">
  <CardHeader className="pb-3">
    <CardTitle className="text-sm font-medium text-gray-200 flex items-center gap-2">
      <Icon size={16} /> Section Name
    </CardTitle>
  </CardHeader>
  <CardContent className="space-y-4">
    {/* content */}
  </CardContent>
</Card>
```

**Card conventions in this system:**
- Override token defaults with concrete classes: `bg-gray-800 border-gray-700`
- `CardTitle` is restyled to `text-sm font-medium` (not the default `text-2xl`) — section titles are small and understated
- Always pair an icon with the card title at `size={16}`
- Use `space-y-3` or `space-y-4` inside `CardContent` for consistent row rhythm

---

### Stat / Data Cell

A recessed data display element — `bg-gray-900` inside a `bg-gray-800` card, creating a sunken effect. Used for metrics, path displays, and key values.

```tsx
{/* Single-value cell */}
<div className="bg-gray-900 p-2 rounded flex flex-col gap-1">
  <span className="text-xs text-gray-400 flex items-center gap-1">
    <Icon size={12} /> Label
  </span>
  <span className="text-sm font-medium text-gray-200">Value</span>
</div>

{/* Two-column grid of stat cells */}
<div className="grid grid-cols-2 gap-2 text-sm">
  <div className="bg-gray-900 p-2 rounded flex flex-col gap-1">...</div>
  <div className="bg-gray-900 p-2 rounded flex flex-col gap-1">...</div>
</div>

{/* Path display cell — with icon and truncation */}
<div className="flex items-center gap-2 text-sm text-gray-200 bg-gray-900 p-2 rounded">
  <FolderTree size={14} className="text-blue-400 flex-shrink-0" />
  <span className="truncate" title={fullValue}>{displayValue}</span>
</div>
```

---

### Badge

For inline status labels, type indicators, and count displays.

```tsx
const badgeVariants = cva(
  "inline-flex items-center rounded-full border px-2.5 py-0.5 text-xs font-semibold transition-colors",
  {
    variants: {
      variant: {
        default:     "border-transparent bg-primary text-primary-foreground",
        secondary:   "border-transparent bg-secondary text-secondary-foreground",
        destructive: "border-transparent bg-destructive text-destructive-foreground",
        outline:     "text-foreground",
        status:      "border-0 text-white",  // background set via className prop
      },
    },
  }
)

// Color-coded status badge:
<Badge variant="status" className="bg-blue-600">Active</Badge>
<Badge variant="status" className="bg-emerald-700">Synced</Badge>
```

The `status` variant removes the border and lets `className` set the background — useful for dynamic or data-driven color coding.

---

## List Row Pattern

Used for items in explorer trees, staging lists, and any selectable list inside a panel.

```tsx
{/* List row — hover reveals action button */}
<div className="flex justify-between items-center group bg-gray-900 p-2 rounded text-xs border border-gray-700/50 hover:bg-gray-800 transition overflow-hidden">
  <div className="flex items-center gap-2 min-w-0 pr-2">
    <FileText size={12} className="text-blue-300 flex-shrink-0" />
    <span className="truncate text-gray-300" title={fullLabel}>{label}</span>
  </div>
  {/* Action — hidden until hover via group-hover */}
  <button className="opacity-0 group-hover:opacity-100 flex-shrink-0 text-gray-500 hover:text-red-400 transition-opacity">
    <X size={14} />
  </button>
</div>
```

**Key patterns:**
- `group` on the row + `group-hover:opacity-100` on the action — reveals controls on hover without layout shift
- `min-w-0` + `truncate` on the label container — required for flex text truncation to work
- `border-gray-700/50` — a half-opacity border that separates rows without being heavy
- Hover state: `hover:bg-gray-800` — one step lighter than `bg-gray-900` base

**Empty state:**
```tsx
<div className="text-xs text-gray-500 text-center py-4 bg-gray-900 rounded border border-dashed border-gray-700">
  Nothing here yet.
</div>
```

---

## Icons

Library: `lucide-react`. All icons are inline SVG, controlled via the `size` prop.

### Sizing conventions

| Context | Size |
|---|---|
| Inline with text / button labels | `size={16}` |
| Small label prefix (stat cell, row) | `size={12}` or `size={14}` |
| Breadcrumb separator | `size={14}` |
| Sidebar / panel toggle | `size={20}` |
| Standalone / prominent indicator | `size={24}` |

### Color conventions

| Role | Color class |
|---|---|
| Default / neutral | inherits text color |
| Navigation / informational | `text-blue-400` |
| File / content item | `text-blue-300` |
| Success / sync indicator | `text-emerald-400` |
| Warning | `text-yellow-500` |
| Destructive / remove | `text-red-400` (on hover only, via `hover:text-red-400`) |
| Muted / structural | `text-gray-400` or `text-gray-500` |

### Recommended icon map (adaptable)

```tsx
import {
  AlertTriangle,  // inline warnings
  ChevronLeft,    // collapse / back
  ChevronRight,   // expand / separator
  FileText,       // file / document items
  Folder,         // directory / group items
  RefreshCcw,     // sync / refresh actions
  Settings,       // configuration
  Wrench,         // tools / utilities
  Server,         // data source / archive
  Grid,           // layout / overview
  Link,           // connections / edges
  Calendar,       // timestamps / dates
  FolderTree,     // path / hierarchy
  Plus,           // add
  Check,          // confirm / success
  X,              // close / remove
  Send,           // submit / export
  Trash2,         // delete
  FolderSync,     // staging / sync queue
} from 'lucide-react'
```

---

## Interactive & State Affordances

### Hover

All interactive elements use `transition-colors` for smooth color changes. Never animate transforms or sizes on hover — keep interactions subtle.

```
text: text-gray-400 → hover:text-white
bg: bg-gray-800 → hover:bg-gray-700
chromatic bg: bg-emerald-900/50 → hover:bg-emerald-800
icon action: text-gray-500 → hover:text-red-400
```

### Selected / Active state

Active navigation items, selected nodes, current breadcrumb segments: `text-blue-400`. Never bold — color alone signals selection.

### Focus

Keyboard focus: `focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2`. Apply via the Button component's base class. Don't add to every element manually — scope to interactive primitives.

### Disabled

`disabled:opacity-50 disabled:pointer-events-none` — reduce opacity, remove interactions. No other change.

### Reveal on hover (group pattern)

For actions that should only appear on row hover (delete, remove, expand):
```tsx
<div className="group ...">
  <button className="opacity-0 group-hover:opacity-100 transition-opacity ...">
    <X size={14} />
  </button>
</div>
```

---

## Alert & Status Patterns

### Inline warning banner (header)

For non-blocking but important system-level warnings. Appears inline with the header content, not as a toast or modal.

```tsx
<div className="flex items-center gap-2 bg-yellow-900/50 text-yellow-500 px-3 py-1 rounded text-sm font-medium border border-yellow-700/50">
  <AlertTriangle size={14} />
  Warning message here.
</div>
```

Note: yellow uses `text-yellow-500` (not `yellow-200`) because `yellow-200` reads too light against the dark background.

### Inline panel alert (within card)

For contextual warnings inside a panel or card — softer than the header banner.

```tsx
<div className="bg-yellow-900/20 text-yellow-400 p-2 rounded text-xs">
  Contextual warning or truncation notice.
</div>
```

`/20` opacity background vs `/50` — panels use a softer version of the same pattern.

### Primary action button (full-width, panel footer)

For the main action in a panel — use a solid color (not the triplet), full-width, in a footer strip.

```tsx
<div className="p-3 bg-gray-900 border-t border-gray-700 mt-auto">
  <button className="w-full flex items-center justify-center gap-2 bg-blue-600 hover:bg-blue-500 text-white p-2 rounded text-sm transition font-medium">
    <Send size={14} /> Submit Action
  </button>
</div>
```

Solid `bg-blue-600` (not the triplet) signals primary/commit — this is the point of no return. The triplet pattern is for mode-switching or system actions; solid color is for submit/confirm.

---

## Summary: The Pattern at a Glance

| Design decision | Rule |
|---|---|
| Theme | Dark-first, `.dark` on `<html>`, no toggle needed |
| Surface depth | gray-900 base → gray-800 elevated → gray-900 sunken |
| Borders | Always `border-gray-700` |
| Text hierarchy | white → gray-200 → gray-300 → gray-400 → gray-500 |
| Brand font | Exo 2, uppercase, wide tracking — title only |
| UI font | Inter — everything else |
| Action color coding | emerald=sync, purple=tools, blue=nav/info, yellow=warn, red=danger |
| Chromatic button formula | `*-900/50` bg + `*-700/50` border + `*-200` text + `hover:*-800` |
| Active/selected | `text-blue-400` |
| Icons | lucide-react, size matched to context (12/14/16/20/24) |
| Hover | `transition-colors`, color shift only — no transform/scale |
| Panel overlay | `absolute`, `backdrop-blur-sm`, `bg-gray-900/90` — never push layout |
| Empty states | Dashed border, gray-900 bg, gray-500 text, centered |

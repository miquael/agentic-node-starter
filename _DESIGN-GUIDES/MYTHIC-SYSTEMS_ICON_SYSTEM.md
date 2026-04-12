# Mythic Systems Icon Design System

This guide outlines how to use and maintain the standardized icon system in the Mythic Systems website.

## Core Component: `FeatureIcon`

All feature/section icons should use the `FeatureIcon` component located at `src/components/ui/FeatureIcon.tsx`.

The system uses a **Semantic Variant** approach. Instead of manually setting borders, shapes, and glows, you select a `variant` that describes the icon's purpose. The component handles the visual styling centrally.

```tsx
import { FeatureIcon } from '../components/ui/FeatureIcon';
import { Zap } from 'lucide-react';

<FeatureIcon 
  icon={Zap} 
  color="cyan" 
  variant="card-icon" 
  size="xl" 
/>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `icon` | `LucideIcon` \| Component | Required | The icon to display. Supports Lucide icons or custom components. |
| `color` | `string` | `'cyan'` | The color theme (see Palette below). |
| `variant` | `IconVariant` | Required | Semantic style variant (see Variants below). |
| `size` | `string` | *(Variant Default)* | Optional override for size. |
| `className` | `string` | `''` | Arbitrary Tailwind classes for overrides (use sparingly). |

## Semantic Variants

The `variant` prop determines the shape, border, glow, and default size.

| Variant | Use Case | Visual Style | Shape | Default Size | Glow? |
|---------|----------|--------------|-------|--------------|-------|
| `section-hero` | Page Headers, Key Stats | **Hero Style**: Faded outline, transparent body, strong glow. | Circle | `xl` (w-20) | Yes |
| `card-icon` | Standard Feature Cards | **Subtle Style**: Faded outline (`/30`), subtle background (`/10`), glow. | Square | `lg` (w-16) | Yes |
| `subtle-card` | Dense grids, "About" sections | **Subtle Style**: Faded outline (`/30`), subtle background (`/10`), *no glow*. | Square | `md` (w-12) | No |
| `process-step` | Linear process steps | **Outline Style**: Solid outline, clear background, *no glow*. | Square | `md` (w-12) | No |
| `process-circle`| Circular process flows | **Subtle Style**: Faded outline, subtle background, *no glow*. | Circle | `xl` (w-20) | No |
| `step-circle` | Numbered process steps | **Subtle Style**: Faded outline, subtle background, *no glow*. | Circle | `lg` (w-16) | No |
| `display` | Home Page "What We Do" | **Hero Style**: Heavy 5px border, strong glow. | Circle | `2xl` (w-28) | Yes |

## Sizes

Dimensions include padding.

| Size | Dimensions | Padding |
|------|------------|---------|
| `sm` | w-10 h-10 | p-2 |
| `md` | w-12 h-12 | p-2.5 |
| `lg` | w-16 h-16 | p-3 |
| `xl` | w-20 h-20 | p-4 |
| `2xl`| w-28 h-28 | p-6 |

## Configuration (`variantConfig`)

The standards are defined in `src/components/ui/FeatureIcon.tsx` within the `variantConfig` object:

```typescript
const variantConfig: Record<IconVariant, {
  shape: 'circle' | 'square';
  defaultSize: 'sm' | 'md' | 'lg' | 'xl' | '2xl';
  borderWidth: string; 
  hasGlow: boolean;
  styleType: 'hero' | 'outline' | 'subtle' | 'solid' | 'transparent';
}> = {
  // ... configuration definitions
}
```

## Color Palette

The system supports the following theme colors. To add a new color, you must update the `colorStyles` object in `FeatureIcon.tsx`.

*   `cyan` (Primary Brand)
*   `purple` (Secondary Brand)
*   `emerald` (Success/Growth)
*   `amber` (Warning/Attention)
*   `amber-dim` (Muted amber variant)
*   `blue` (Tech/Trust)
*   `orange` (Energy)
*   `indigo` (Deep Tech)
*   `white` (Neutral/Inverse)
*   `green`
*   `red`
*   `pink`
*   `yellow`
*   `gray`

## How to Make Changes

### Adjusting a Style Globally
To change how *all* "Card Icons" look (e.g., changing their border width), edit the `card-icon` entry in the `variantConfig` object in `src/components/ui/FeatureIcon.tsx`.

### Adding a New Variant
1.  Open `src/components/ui/FeatureIcon.tsx`.
2.  Add the new variant name to the `IconVariant` type definition.
3.  Add the configuration object for the new variant in `variantConfig`.

### Adding a New Color
1.  Open `src/components/ui/FeatureIcon.tsx`.
2.  Update the `FeatureIconProps` interface to include the new color name.
3.  Add the new color key to the `colorStyles` object with specific tailwind classes for `outline`, `subtle`, `solid`, and `hero` styles.

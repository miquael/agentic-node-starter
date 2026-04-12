# UI Design & Aesthetics Reference

This document serves as a reference for adopting the premium look and feel of the current application into your new 2D/3D Astrological Ephemeris Visualization app. While the core architecture (Scanner/Server/Viewer) and 3D engines might differ, the visual polish can be carried over identically to maintain a cohesive, high-quality user experience.

## 1. Design Language & Aesthetics

The application leans into a modern, data-dense "dark mode" aesthetic suitable for technical or complex data visualization.

### Key Visual Characteristics
- **Dark Theme Priority:** The primary background is deeply dark (`bg-gray-900`) allowing the bright 3D elements and glowing UI components to stand out.
- **Glassmorphism:** Overlapping interface elements (like floating sidebars and modals) utilize translucent backgrounds with background blurring.
  - *Example Pattern:* `bg-gray-900/90 backdrop-blur-sm` paired with subtle borders.
- **Micro-interactions:** Buttons and toggles use subtle background and text color shifts on hover.
  - *Example Patter:* `transition-transform duration-300 ease-in-out` on sliding panels, `hover:text-white hover:bg-gray-700` on icon buttons.
- **Rounded Edges:** The standard border-radius across panels, buttons, and cards is a clean, medium curve (`--radius: 0.5rem;` / `rounded-lg`).

## 2. Core Color Palette (CSS Variables)

The UI uses a flexible CSS variable system (likely derived from shadcn/ui) that maps directly to Tailwind CSS utilities. This makes swapping themes seamless.

### Standard Dark Mode Variables
```css
:root {
  /* Core Spacing / Structure */
  --radius: 0.5rem;
}

.dark {
  /* Core Backgrounds */
  --background: 222.2 84% 4.9%;    /* Very dark blue-gray */
  --foreground: 210 40% 98%;       /* Near white for text */

  /* Surface / Panels */
  --card: 222.2 84% 4.9%;
  --card-foreground: 210 40% 98%;
  --popover: 222.2 84% 4.9%;
  --popover-foreground: 210 40% 98%;

  /* Action / Accent Colors */
  --primary: 210 40% 98%;
  --primary-foreground: 222.2 47.4% 11.2%;
  --secondary: 217.2 32.6% 17.5%;
  --secondary-foreground: 210 40% 98%;
  
  /* Structural Lines */
  --border: 217.2 32.6% 17.5%;     /* Subtle borders for panels */
  --ring: 212.7 26.8% 83.9%;       /* Focus rings */
}
```

## 3. UI Component System

The application relies heavily on encapsulated UI components (like Radix UI / Shadcn UI). When building the new application, you should create these identical primitives to keep the design cohesive:

### Common Component Primitives
*   **Card Container (`Card`, `CardHeader`, `CardContent`):** Used for segregating chunks of data (e.g., planetary positions, aspect tables).
    *   *Styling:* `rounded-lg border bg-card text-card-foreground shadow-sm`
*   **Action Elements (`Button`, `Slider`, `Toggle`):** Used for manipulating the 3D view and data parameters.
    *   *Styling:* Uses the `--primary` and `--secondary` accent colors with `clsx` and `tailwind-merge` to handle states flexibly.
*   **Badges / Indicators (`Badge`):** Used for small data points (e.g., highlighting a specific planetary aspect or dignity).

## 4. Typography & Iconography

*   **Icons:** The application utilizes **`lucide-react`**. This icon set is minimal, highly legible, and fits perfectly with the sharp, technical aesthetic of a visualization tool. Examples of usage include `ChevronLeft`/`ChevronRight` for panel toggling, and standard settings icons.
*   **Typography:** Interface elements use uppercase, tracking-wide text for section headers to feel more like a technical dashboard.
    *   *Example Pattern (Sidebar Header):* `text-sm font-semibold text-gray-200 uppercase tracking-wider`

## 5. Layout Shell Structure

You can drop the following structural concept directly into the new project to maintain the exact same floating overlay feel relative to the 3D canvas:

```tsx
// AppLayout Shell Example
<div className="relative w-full h-full min-h-0 overflow-hidden bg-gray-900">
  
  {/* The 3D Engine Frame remains fully positioned in the background */}
  <div className="absolute inset-0 z-0">
    <Astrology3DCanvas /> 
  </div>

  {/* Panels float over the 3D Engine using fixed/absolute positioning */}
  <div className="absolute inset-y-0 left-0 z-20 flex pointer-events-none">
     {/* Wrap interactable elements in pointer-events-auto */}
     <div className="w-80 h-full bg-gray-900/90 backdrop-blur-sm border-r border-gray-700 pointer-events-auto">
        {/* Left Side Controls (e.g. Ephemeris Layers) */}
     </div>
  </div>

</div>
```

## Conclusion

By copying the CSS variables (to form your color tokens), standardizing on `lucide-react` for iconography, and using standard tailwind classes applied with "glassmorphism" (`backdrop-blur-sm`, `bg-gray-900/90`), you can rapidly bootstrap the new application to look indistinguishably premium and related to this original project.

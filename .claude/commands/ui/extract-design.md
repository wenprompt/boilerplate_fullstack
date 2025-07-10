# CREATE DESIGN SYSTEM JSON

- UI TO ANALYZE: $ARGUMENTS

## INPUT

Screenshots provided in `$ARGUMENTS` for visual analysis.

## GOAL

You goal is to extract a generalized and reusable design system from the screenshots provided in `$ARGUMENTS`, **without including specific image content**, so that frontend developers or AI Agents can reference the JSON as a style foundation for building consistent UIs for the entire project.

## CONSTRAINTS

### Content Restrictions:

- **DO NOT** extract specific content (text, logos, icons)
- Focus purely on design principles, structure, and styles

### Technical Requirements (Tailwind v4, shadcn/ui):

- **Color System**: Extract colors in OKLCH format (e.g., `oklch(0.971 0.013 17.38)`) as Tailwind v4 now uses OKLCH for better color accuracy and perceptual uniformity
- **CSS Variables Format**: Structure colors as CSS custom properties that work with the new `@theme` directive:
  - Use `--color-[name]` format for Tailwind compatibility (e.g., `--color-primary`, `--color-background`)
  - Support both light and dark mode definitions using `:root` and `.dark` selectors
- **No Config File**: Since Tailwind v4 eliminates tailwind.config.js, all theme configuration should be CSS-based using `@theme` directive
- **shadcn/ui Color Convention**: Follow shadcn/ui's background/foreground pattern:
  - Each color should have a base color and corresponding foreground color
  - Format: `--primary` and `--primary-foreground`, `--background` and `--foreground`
- **Spacing**: Map to Tailwind's default spacing scale but note that some utilities have been renamed in v4:
  - `shadow-sm` → `shadow-xs`, `shadow` → `shadow-sm`
  - `rounded-sm` → `rounded-xs`, `rounded` → `rounded-sm`
  - `blur-sm` → `blur-xs`, `blur` → `blur-sm`
- **Typography**: Extract font definitions compatible with CSS variable format:
  - Use `--font-[family]` format (e.g., `--font-sans`, `--font-display`)
  - Support Tailwind's default font stacks as fallbacks
- **Border Radius**: Extract radius values that work with shadcn/ui's `--radius` variable system
- **Component Variants**: Structure components to match shadcn/ui's approach using CSS variables for theming rather than utility classes
- **CSS Variable Syntax**: Use the new Tailwind v4 syntax for CSS variables in utilities:
  - `bg-(--my-color)` instead of `bg-[var(--my-color)]`
  - Support arbitrary value syntax with parentheses
- **Theme Inline Support**: Structure variables to work with `@theme inline` directive for better performance
- **Dark Mode**: Use selector-based dark mode (`.dark`) as per shadcn/ui convention
- **Accessibility**: Ensure color contrast meets WCAG guidelines, especially important with OKLCH color space
- **Use Context7 MCP tool** to find the latest documentation for Tailwind V4 and shadcn/ui to help with your coding.

# TASK

1. Analyze the screenshots given in `$ARGUMENTS` to infer:

   - Color Palatte
   - Typography rules
   - Spacing guidelines
   - Layout structure (grids, cards, containers, etc.)
   - UI components (buttons, inputs, tables, etc.)
   - Border radius, shadows, and other visual styling patterns

2. Create a `ui-design.json` file that follow the rules, contraints and technical requirements.

3. Output to: `PRPs/designs/ui-design.json`.

4. Create a `ascsii-layout.md` file that follows the layout of the screenshot

5. Output to: `PRPs/designs/ascsii-layout.md`.

## EXPECTED OUTPUT FORMAT

### ui-design.json

```JSON
{
  "metadata": {
    "tailwindVersion": "v4",
    "colorFormat": "oklch",
    "framework": "shadcn/ui",
    "darkModeStrategy": "selector"
  },
  "cssVariables": {
    "light": {
      ":root": {
        "--background": "oklch(1 0 0)",
        "--foreground": "oklch(0.145 0 0)",
        "--primary": "oklch(0.205 0 0)",
        "--primary-foreground": "oklch(0.985 0 0)",
        "--radius": "0.625rem"
      }
    },
    "dark": {
      ".dark": {
        "--background": "oklch(0.145 0 0)",
        "--foreground": "oklch(0.985 0 0)"
      }
    }
  },
  "themeDirective": {
    "@theme inline": {
      "--color-background": "var(--background)",
      "--color-foreground": "var(--foreground)",
      "--color-primary": "var(--primary)",
      "--color-primary-foreground": "var(--primary-foreground)",
      "--font-sans": "ui-sans-serif, system-ui, sans-serif",
      "--radius-lg": "var(--radius)"
    }
  },
  "components": {
    "button": {
      "baseStyles": "Uses CSS variables for theming",
      "variants": "Defined through CSS variables, not utility classes"
    }
  }
}
```

### ascsii-layout.md

```ascii
┌─────────────────────────────────────────────────────────────────┐
│                        NAVIGATION BAR                          │
│  [Home] [Membership] [Style Guide] [•••]    [🔍] [Sign in] [Sign up] │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                        MAIN CONTENT AREA                       │
│                                                                 │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌────────────┐ │
│  │   [IMAGE]    │ │   [IMAGE]    │ │   [IMAGE]    │ │  [IMAGE]   │ │
│  │              │ │              │ │              │ │            │ │
│  │              │ │              │ │              │ │            │ │
│  ├──────────────┤ ├──────────────┤ ├──────────────┤ ├────────────┤ │
│  │ Card Title   │ │ Card Title   │ │ Card Title   │ │Card Title  │ │
│  │ Author Name  │ │ Author Name  │ │ Author Name  │ │Author Name │ │
│  │              │ │              │ │              │ │            │ │
│  │   [BADGE]    │ │   [BADGE]    │ │   [BADGE]    │ │  [BADGE]   │ │
│  └──────────────┘ └──────────────┘ └──────────────┘ └────────────┘ │
│                                                                 │
│  ┌─────────────────────────────┐ ┌───────────────────────────────┐ │
│  │                             │ │                               │ │
│  │        [LARGE IMAGE]        │ │        ARTICLE CONTENT        │ │
│  │                             │ │                               │ │
│  │                             │ │  ┌─────────┐                  │ │
│  │                             │ │  │ [BADGE] │ Article Title    │ │
│  │                             │ │  └─────────┘                  │ │
│  │                             │ │                               │ │
│  │                             │ │  Author Info • Date • Read   │ │
│  │                             │ │                               │ │
│  └─────────────────────────────┘ └───────────────────────────────┘ │
│                                                                 │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐              │
│  │   [IMAGE]    │ │   [IMAGE]    │ │   [IMAGE]    │              │
│  │              │ │              │ │              │              │
│  │              │ │              │ │              │              │
│  ├──────────────┤ ├──────────────┤ ├──────────────┤              │
│  │ Card Title   │ │ Card Title   │ │ Card Title   │              │
│  │ Author Name  │ │ Author Name  │ │ Author Name  │              │
│  │              │ │              │ │              │              │
│  │   [BADGE]    │ │   [BADGE]    │ │   [BADGE]    │              │
│  └──────────────┘ └──────────────┘ └──────────────┘              │
│                                                                 │
│                      ┌─────────────────┐                        │
│                      │  [Load more]    │                        │
│                      └─────────────────┘                        │
└─────────────────────────────────────────────────────────────────┘

LEGEND:
┌─┐ = Container borders
│ │ = Content boundaries
=== = Section dividers
[BADGE] = Category/type indicators
[IMAGE] = Content images/media
[BUTTON] = Interactive elements
```

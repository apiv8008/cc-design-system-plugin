---
name: exante-cc-theme
description: Use when the project uses --cc-* CSS tokens, bg-cc-* Tailwind classes, @exante/cc-design-system imports, or Exante brand colors. Covers brand identity, token rules, Tailwind setup, and React components (when applicable).
user-invocable: true
---

# Exante CC Design System

## Brand Identity

Exante is a financial technology company. The visual identity is **clean, minimal, and professional** — green and grey on white. Avoid flashy, overly decorated, or trendy design choices.

### Primary brand colors (must use tokens — never hardcode)

| Color | Hex | Token | Usage |
|-------|-----|-------|-------|
| Exante Green | `#007f39` | `--cc-primary-action` | Primary actions, links, accents |
| Dark text | `#242b2d` | `--cc-text-primary` | Body text, headings |
| Secondary text | `#4e5d60` | `--cc-text-secondary` | Muted text, captions |

### Additional greens (available for accents)
- `#209f59` — lighter green
- `#26bf6b` — lightest green

### Grey scale
`#242b2d` → `#4e5d60` → `#a0afb3` → `#b8c3c6` → `#dbe1e2` → `#f1f3f4`

These are the core brand palette. Green + grey + white. Keep it restrained.

### UI semantic colors (available, not mandatory)
The design system also provides red, yellow, and blue for UI states. These are **not brand colors** — use them only when you need explicit semantic meaning:
- Red (`--cc-radical`) — destructive actions, errors
- Yellow (`--cc-warning`) — warnings
- Blue (`--cc-source`) — informational

Do not overuse these. They should appear sparingly for meaning, not decoration.

### Font
The design system uses **Inter** (400, 500, 600). This is bundled in `@exante/cc-design-system/styles`.

### Icons
Use any public icon library (Lucide, Heroicons, Phosphor, etc.) as you normally would. The design system does not enforce a specific icon set.

### Dark mode
Token values switch automatically when `.dark` is on the root element. No manual handling needed.

---

## What to enforce vs. leave open

| Enforce | Leave open (creative freedom) |
|---------|-------------------------------|
| Brand colors via tokens | Spacing and padding |
| Text color hierarchy | Border radius |
| Font family (Inter) | Layout density and composition |
| Dark mode mechanism | Component dimensions |
| Semantic color meaning | Surface tints and backgrounds beyond base |

Do NOT lock down spacing, radius, or layout. These should feel natural to each app.

---

## Import Paths

| What | Import from |
|------|-------------|
| Global styles (CSS) | `@exante/cc-design-system/styles` |
| Tailwind preset | `@exante/cc-design-system/tailwind-preset` |
| React components | `@exante/cc-design-system` |

---

## Tailwind Setup

```js
import ccPreset from '@exante/cc-design-system/tailwind-preset';

export default {
  presets: [ccPreset],
  content: [
    './src/**/*.{js,ts,jsx,tsx}',
    './node_modules/@exante/cc-design-system/dist/**/*.{js,mjs}',
  ],
  darkMode: 'class',
};
```

---

## React Components

**Only applies when the project has react in package.json.**

Before building any UI control, check if it already exists. See `references/components.md` for full API.

| Category | Components |
|----------|-----------|
| Buttons | `Button` (5 variants, 3 sizes, icon slots, BG mode) |
| Typography | `H1`–`H6` |
| Tabs | `Tabs` (WAI-ARIA, badges, icons, skeleton) |
| Form controls | `Input`, `Checkbox`, `Radio`, `Switcher` |
| Feedback | `Toast`, `Alert` |
| Status | `StatusIndicator` (20 statuses, 6 color groups) |
| Overlays | `Tooltip` (desktop popover + mobile bottom sheet) |
| Data tables | `TableHeaderCell`, `FilterLabel`, `FilterRow`, `ColumnPicker` |
| Date range | `Calendar` (dual-panel, Monday-first) |
| Navigation | `Pagination` (responsive, lines-per-page, go-to-page) |
| Error pages | `ErrorPage` (400–503) |

All imported from `@exante/cc-design-system`. Never import from internal paths.

---

## Gotchas

**Hardcoded hex values.** Claude defaults to hex. Always use tokens for brand colors:
- `#007f39` → `--cc-primary-action` / `bg-cc-primary-action`
- `#242b2d` → `--cc-text-primary` / `text-cc-text-primary`

**Tailwind arbitrary values for brand colors.** Never `text-[#007f39]` — use `text-cc-primary-action`.

**Overusing semantic colors.** Red, yellow, blue are for meaning (error, warning, info). Don't use them as decoration or to "add color" to layouts. The brand is green + grey.

**Recreating existing React components.** Don't build a custom button, pagination, date picker, or form control if one exists in the component table above.

**Internal import paths.** Never import from `src/` or `dist/`:
```ts
// wrong
import { Button } from '@exante/cc-design-system/src/components/Button';
// correct
import { Button } from '@exante/cc-design-system';
```

**Overly rigid layouts.** Don't force the same spacing, radius, or density on every app. The tokens handle colors and meaning — layout is up to the app.

**className overrides that break dark mode.** Don't override token-based styles with static colors — the override won't adapt to dark mode.

**Missing darkMode: 'class' in Tailwind config.** Without it, dark mode tokens won't switch.

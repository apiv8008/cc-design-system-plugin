---
name: exante-cc-theme
description: Use when the project uses --cc-* CSS tokens, bg-cc-* Tailwind classes, @exante/cc-design-system imports, or Exante brand colors. Covers token rules, Tailwind setup, and React components (when applicable).
user-invocable: true
---

# Exante CC Design System

## Token Usage

Always use `--cc-*` CSS custom properties. Never hardcode brand colors as hex values.

**In plain CSS:**
```css
/* correct */
color: var(--cc-text-primary);
background: var(--cc-surface-primary);

/* wrong */
color: #242b2d;
background: #ffffff;
```

**In Tailwind classes:**
```html
<!-- correct -->
<p class="text-cc-text-primary bg-cc-surface-primary">...</p>

<!-- wrong -->
<p class="text-[#242b2d] bg-white">...</p>
```

**Brand colors that must NOT be hardcoded:**

| Color | Hex | Correct token |
|-------|-----|---------------|
| Primary / green | `#007f39` | `--cc-primary-action` / `bg-cc-primary-action` |
| Radical / red | `#d75237` | `--cc-radical` / `bg-cc-radical` |
| Warning / yellow | `#ea9c0b` | `--cc-warning` / `bg-cc-warning` |
| Source / blue | `#256690` | `--cc-source` / `bg-cc-source` |

Dark mode switches automatically when `.dark` is on the root element.

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
| Badges | `Badge` (5 variants, indicator dot, loading) |
| Typography | `H1`–`H6` |
| Tabs | `Tabs` (WAI-ARIA, badges, icons, skeleton) |
| Form controls | `Input`, `Checkbox`, `Radio`, `Switcher` |
| Feedback | `Toast`, `Alert` |
| Status | `StatusIndicator` (20 statuses, 6 color groups) |
| Overlays | `Tooltip` (desktop popover + mobile bottom sheet) |
| Data tables | `TableHeaderCell`, `FilterLabel`, `FilterRow`, `ColumnPicker` |
| Date range | `Calendar` (dual-panel, Monday-first) |
| Navigation | `Pagination` (responsive, lines-per-page, go-to-page) |
| Error pages | `ErrorPage` (400, 401, 403, 404, 500, 502, 503) |

All imported from `@exante/cc-design-system`.

---

## Gotchas

**Hardcoded hex values.** Claude defaults to hex colors. Always map to tokens:
- `#007f39` → `--cc-primary-action` / `bg-cc-primary-action`
- `#d75237` → `--cc-radical` / `text-cc-radical`
- `#ea9c0b` → `--cc-warning` / `border-cc-warning`
- `#256690` → `--cc-source` / `text-cc-source`

**Tailwind arbitrary values for design system colors.** Never use `text-[#526266]` — use `text-cc-text-secondary`.

**Recreating existing components.** Do not build a custom button, modal, pagination, date picker, or form control if one exists in the table above. Use the design system component.

**Internal import paths.** Never import from `src/` or `dist/` directly:
```ts
// wrong
import { Button } from '@exante/cc-design-system/src/components/Button';
import { Button } from '@exante/cc-design-system/dist/index.js';
// correct
import { Button } from '@exante/cc-design-system';
```

**Missing darkMode: 'class' in Tailwind config.** Without it, dark mode tokens won't switch.

**className overrides that break dark mode.** Don't override token-based styles with static colors via className — the override won't adapt to dark mode.

---
name: exante-cc-theme
description: Exante CC Design System rules — use when building UI with @exante/cc-design-system tokens, components, or Tailwind preset.
user-invocable: true
---

# CC Design System — Rules

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

Dark mode token values switch automatically when the `.dark` class is on the root element.

---

## Import Paths

| What | Import from |
|------|-------------|
| Components (React) | `@exante/cc-design-system` |
| Tailwind preset | `@exante/cc-design-system/tailwind-preset` |
| Global styles (CSS) | `@exante/cc-design-system/styles` |

**Correct:**
```ts
import { Button, Badge } from '@exante/cc-design-system';
import ccPreset from '@exante/cc-design-system/tailwind-preset';
```
```css
@import '@exante/cc-design-system/styles';
```

**Wrong — never import from internal paths:**
```ts
// do not do this
import { Button } from '@exante/cc-design-system/src/components/Button';
import { Button } from '@exante/cc-design-system/dist/index.js';
```

---

## Tailwind Setup

Consumer `tailwind.config.js` must:

1. Import and add `ccPreset` to `presets`
2. Include the dist folder in `content` so Tailwind scans component class names
3. Set `darkMode: 'class'`

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

## Available Components (React)

Use these instead of building custom equivalents. All imported from `@exante/cc-design-system`.

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

---

## Anti-Patterns

**Do NOT recreate components that already exist in the design system.**

**Do NOT hardcode Exante brand colors.**
```tsx
// wrong
<div className="bg-[#007f39] text-[#ffffff]">
// correct
<div className="bg-cc-primary-action text-cc-inverse">
```

**Do NOT import from internal paths.**
```ts
// wrong
import { Button } from '@exante/cc-design-system/src/components/Button/Button';
// correct
import { Button } from '@exante/cc-design-system';
```

**Do NOT use Tailwind arbitrary values for design system colors.**
```tsx
// wrong — <p className="text-[#526266]">
// correct — <p className="text-cc-text-secondary">
```

**Do NOT use `bg-[#007f39]` — use `bg-cc-primary-action`.**
**Do NOT use `text-[#d75237]` — use `text-cc-radical`.**
**Do NOT use `border-[#ea9c0b]` — use `border-cc-warning`.**
**Do NOT use `text-[#256690]` — use `text-cc-source`.**

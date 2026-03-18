---
name: exante-cc-theme
description: Exante CC Design System — token usage, Tailwind preset, and color rules. Use when building any UI with @exante/cc-design-system styles, --cc-* CSS tokens, or Tailwind cc-* classes. Framework-agnostic.
user-invocable: true
---

# Exante CC Theme — Rules

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
| Tailwind preset | `@exante/cc-design-system/tailwind-preset` |
| Global styles (CSS) | `@exante/cc-design-system/styles` |

```css
@import '@exante/cc-design-system/styles';
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

## Anti-Patterns

**Do NOT hardcode Exante brand colors.**
```css
/* wrong */
background: #007f39;
color: #d75237;

/* correct */
background: var(--cc-primary-action);
color: var(--cc-radical);
```

**Do NOT use Tailwind arbitrary values for design system colors.**
```html
<!-- wrong -->
<p class="text-[#526266] bg-[#007f39]">

<!-- correct -->
<p class="text-cc-text-secondary bg-cc-primary-action">
```

**Do NOT use `bg-[#007f39]` — use `bg-cc-primary-action`.**
**Do NOT use `text-[#d75237]` — use `text-cc-radical`.**
**Do NOT use `border-[#ea9c0b]` — use `border-cc-warning`.**
**Do NOT use `text-[#256690]` — use `text-cc-source`.**

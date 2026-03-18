---
name: exante-cc-components
description: Exante CC Design System React components — use when the project has React and imports from @exante/cc-design-system. Component API, import paths, and anti-patterns for Button, Badge, Tabs, Input, etc.
user-invocable: false
---

# Exante CC Components — React

Only applies to projects using React with `@exante/cc-design-system`.

## Import Path

```ts
import { Button, Badge, Tabs } from '@exante/cc-design-system';
```

**Never import from internal paths:**
```ts
// wrong
import { Button } from '@exante/cc-design-system/src/components/Button';
import { Button } from '@exante/cc-design-system/dist/index.js';
```

---

## Available Components

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

## Component API

### Button
```tsx
<Button variant="primary" size="M" state="default" bg={true} iconLeft={<Icon />} iconRight={<Icon />}>Label</Button>
```
- `variant`: `'primary'` | `'secondary'` | `'radical'` | `'source'` | `'ghost'`
- `size`: `'M'` | `'S'` | `'XS'`
- `state`: `'default'` | `'disabled'` | `'loading'` | `'skeleton'`
- `bg`: `boolean` — false renders text-only
- `iconLeft` / `iconRight`: `React.ReactNode`

### Badge
```tsx
<Badge variant="default" size="M" indicator loading>Label</Badge>
```
- `variant`: `'default'` | `'ghost'` | `'source'` | `'warning'` | `'radical'`
- `size`: `'S'` | `'M'`
- `indicator`: `boolean` — dot after label
- `loading`: `boolean` — spinner before label

### Typography (H1–H6)
```tsx
<H1>Page Title</H1>
```

### Tabs
```tsx
<Tabs tabs={[{ id, label, content, disabled?, badge?, iconLeft?, indicator?, description?, skeleton? }]} defaultActiveId="id" />
```

### Input
```tsx
<Input title="Label" size="M" validation="default" subMessage="Help" tags={[{id, label}]} onTagRemove={fn} showDropdownArrow showInfoIcon disabled skeleton />
```
- `size`: `'M'` | `'S'`
- `validation`: `'default'` | `'source'` | `'warning'` | `'radical'`

### Checkbox
```tsx
<Checkbox label="Text" colorType="default" checked={bool} onChange={fn} bg description="Desc" showInfo disabled skeleton />
```
- `colorType`: `'default'` | `'warning'` | `'radical'`

### Radio
```tsx
<Radio label="Text" colorType="default" checked={bool} onChange={fn} bg description="Desc" name="group" value="val" disabled skeleton />
```
- `colorType`: `'default'` | `'warning'` | `'radical'`

### Switcher
```tsx
<Switcher label="Text" colorType="default" checked={bool} onChange={fn} bg titleLeft showInfo disabled skeleton />
```
- `colorType`: `'default'` | `'warning'` | `'radical'`

### Toast
```tsx
<Toast heading="Title" description="Body" dateTime="10:30 AM" onClose={fn} skeleton />
```

### Alert
```tsx
<Alert variant="source">Message</Alert>
```
- `variant`: `'source'` | `'warning'` | `'radical'` | `'skeleton'`

### StatusIndicator
```tsx
<StatusIndicator status="Active" />
```
20 values: `Processed`, `Filled`, `Active`, `Placing`, `Booked In BO`, `Failed`, `Rejected`, `Canceled`, `Settled`, `Pending`, `Funds Rejected`, `Requested`, `Experation`, `Funds are locked`, `Processing`, `Ready for booking`, `Checks required`, `Working`, `New`, `Archived`

### Tooltip
```tsx
<Tooltip device="desktop" arrow="bottom" head="Title" description="Body" buttons={<>...</>} />
<Tooltip device="mobile" headerColor="source" head="Title" description="Body" />
```
- `arrow`: `'top'` | `'bottom'` | `'left'` | `'right'` (desktop)
- `headerColor`: `'default'` | `'source'` | `'warning'` | `'radical'` | `'none'` (mobile)

### Pagination
```tsx
<Pagination totalPages={20} currentPage={1} onPageChange={fn} linesPerPage={25} linesPerPageOptions={[10,25,50,100]} onLinesPerPageChange={fn} onGoToPage={fn} responsive skeleton />
```

### TableHeaderCell
```tsx
<TableHeaderCell label="Name" size="M" state="default" leftIcon={<Icon />} badge={3} showIndicator sortDirection="asc" onClick={fn} />
```
- `size`: `'M'` | `'S'` | `'M Arrow'`
- `state`: `'default'` | `'hover'` | `'focus'` | `'skeleton'` | `'warning'` | `'disabled'`

### FilterLabel
```tsx
<FilterLabel title="Filters" activeCount={3} compact />
```

### FilterRow
```tsx
<FilterRow type="text" label="Name" value={val} onValueChange={fn} onRemove={fn} />
```
- `type`: `'text'` | `'date'` | `'checkbox'` | `'dropdown'` | `'range'` | `'search'` | `'general'`

### ColumnPicker
```tsx
<ColumnPicker columns={[{id, label, checked}]} onColumnsChange={fn} activeView="table" onViewChange={fn} />
```

### Calendar
```tsx
<Calendar startDate={date} endDate={date} onRangeChange={fn} initialMonth={date} minDate={date} maxDate={date} />
```

### ErrorPage
```tsx
<ErrorPage code={404} onHome={fn} onReload={fn} />
```
Codes: `400` | `401` | `403` | `404` | `500` | `502` | `503`

---

## Anti-Patterns

**Do NOT recreate components that already exist above.**

**Do NOT import from internal paths.**
```ts
// wrong
import { Button } from '@exante/cc-design-system/src/components/Button/Button';
// correct
import { Button } from '@exante/cc-design-system';
```

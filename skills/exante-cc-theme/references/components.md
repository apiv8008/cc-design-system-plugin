# Component API Reference

All components imported from `@exante/cc-design-system`.

## Button
```tsx
<Button variant="primary" size="M" state="default" bg={true} iconLeft={<Icon />} iconRight={<Icon />}>Label</Button>
```
- `variant`: `'primary'` | `'secondary'` | `'radical'` | `'source'` | `'ghost'`
- `size`: `'M'` | `'S'` | `'XS'`
- `state`: `'default'` | `'disabled'` | `'loading'` | `'skeleton'`
- `bg`: `boolean` — false renders text-only
- `iconLeft` / `iconRight`: `React.ReactNode`

## Badge
```tsx
<Badge variant="default" size="M" indicator loading>Label</Badge>
```
- `variant`: `'default'` | `'ghost'` | `'source'` | `'warning'` | `'radical'`
- `size`: `'S'` | `'M'`
- `indicator`: `boolean` — dot after label
- `loading`: `boolean` — spinner before label

## Typography (H1–H6)
```tsx
<H1>Page Title</H1>
```

## Tabs
```tsx
<Tabs tabs={[{ id, label, content, disabled?, badge?, iconLeft?, indicator?, description?, skeleton? }]} defaultActiveId="id" />
```

## Input
```tsx
<Input title="Label" size="M" validation="default" subMessage="Help" tags={[{id, label}]} onTagRemove={fn} showDropdownArrow showInfoIcon disabled skeleton />
```
- `size`: `'M'` | `'S'`
- `validation`: `'default'` | `'source'` | `'warning'` | `'radical'`

## Checkbox
```tsx
<Checkbox label="Text" colorType="default" checked={bool} onChange={fn} bg description="Desc" showInfo disabled skeleton />
```
- `colorType`: `'default'` | `'warning'` | `'radical'`

## Radio
```tsx
<Radio label="Text" colorType="default" checked={bool} onChange={fn} bg description="Desc" name="group" value="val" disabled skeleton />
```
- `colorType`: `'default'` | `'warning'` | `'radical'`

## Switcher
```tsx
<Switcher label="Text" colorType="default" checked={bool} onChange={fn} bg titleLeft showInfo disabled skeleton />
```
- `colorType`: `'default'` | `'warning'` | `'radical'`

## Toast
```tsx
<Toast heading="Title" description="Body" dateTime="10:30 AM" onClose={fn} skeleton />
```

## Alert
```tsx
<Alert variant="source">Message</Alert>
```
- `variant`: `'source'` | `'warning'` | `'radical'` | `'skeleton'`

## StatusIndicator
```tsx
<StatusIndicator status="Active" />
```
20 values: `Processed`, `Filled`, `Active`, `Placing`, `Booked In BO`, `Failed`, `Rejected`, `Canceled`, `Settled`, `Pending`, `Funds Rejected`, `Requested`, `Experation`, `Funds are locked`, `Processing`, `Ready for booking`, `Checks required`, `Working`, `New`, `Archived`

## Tooltip
```tsx
<Tooltip device="desktop" arrow="bottom" head="Title" description="Body" buttons={<>...</>} />
<Tooltip device="mobile" headerColor="source" head="Title" description="Body" />
```
- `arrow`: `'top'` | `'bottom'` | `'left'` | `'right'` (desktop)
- `headerColor`: `'default'` | `'source'` | `'warning'` | `'radical'` | `'none'` (mobile)

## Pagination
```tsx
<Pagination totalPages={20} currentPage={1} onPageChange={fn} linesPerPage={25} linesPerPageOptions={[10,25,50,100]} onLinesPerPageChange={fn} onGoToPage={fn} responsive skeleton />
```

## TableHeaderCell
```tsx
<TableHeaderCell label="Name" size="M" state="default" leftIcon={<Icon />} badge={3} showIndicator sortDirection="asc" onClick={fn} />
```
- `size`: `'M'` | `'S'` | `'M Arrow'`
- `state`: `'default'` | `'hover'` | `'focus'` | `'skeleton'` | `'warning'` | `'disabled'`

## FilterLabel
```tsx
<FilterLabel title="Filters" activeCount={3} compact />
```

## FilterRow
```tsx
<FilterRow type="text" label="Name" value={val} onValueChange={fn} onRemove={fn} />
```
- `type`: `'text'` | `'date'` | `'checkbox'` | `'dropdown'` | `'range'` | `'search'` | `'general'`

## ColumnPicker
```tsx
<ColumnPicker columns={[{id, label, checked}]} onColumnsChange={fn} activeView="table" onViewChange={fn} />
```

## Calendar
```tsx
<Calendar startDate={date} endDate={date} onRangeChange={fn} initialMonth={date} minDate={date} maxDate={date} />
```

## ErrorPage
```tsx
<ErrorPage code={404} onHome={fn} onReload={fn} />
```
Codes: `400` | `401` | `403` | `404` | `500` | `502` | `503`

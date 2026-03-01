# Page Scroll Preservation

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | medium | Preserve scroll for list/detail workflows where continuity matters | preserveScroll, scroll, navigation, workflow |

Use `preserveScroll` for revisits where users should retain visual position.

## Agent Directives

- Trigger: list-heavy pages with frequent filter/reload interactions.
- Must: set `preserveScroll: true` when continuity matters.
- Must Not: reset viewport unnecessarily after same-page updates.
- Auto: pair with partial reload for table interactions.

## Bad Example

```ts
router.get('/users', filters)
```

## Good Example

```ts
router.get('/users', filters, {
  preserveScroll: true,
  preserveState: true,
})
```

## Why

- Improves navigation continuity.
- Reduces reorientation time in data-heavy pages.

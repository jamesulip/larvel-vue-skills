# Page Partial Reloads

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Use partial reload options for same-page data refinements | partial-reloads, only, except, reload |

Use `only`/`except` and same-page reload behavior for efficient updates.

## Agent Directives

- Trigger: same-page filter/search/sort/pagination updates.
- Must: use partial reload options (`only` or `except`).
- Must Not: trigger full prop reload when only subset changed.
- Auto: combine with `preserveState` and `preserveScroll` for dashboard lists.

## Bad Example

```ts
router.get('/users', filters)
```

## Good Example

```ts
router.get('/users', filters, {
  only: ['users', 'filters', 'meta'],
  preserveState: true,
  preserveScroll: true,
})
```

## Why

- Reduces payload size.
- Keeps expensive pages responsive.

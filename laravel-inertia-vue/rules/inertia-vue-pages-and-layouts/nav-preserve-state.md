# Preserve State on Navigation

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Preserve component state for workflow-heavy interactions | preserveState, filters, forms, list-detail |

Use `preserveState` where revisits should keep local UI context.

## Agent Directives

- Trigger: list/detail/filter/search revisits.
- Must: set `preserveState: true` when local context should remain.
- Must Not: reset transient state unless explicitly requested.
- Auto: pair with `preserveScroll: true` for data-heavy lists.

## Bad Example

```ts
router.get('/users', filters)
```

## Good Example

```ts
router.get('/users', filters, {
  preserveState: true,
  preserveScroll: true,
})
```

## Why

- Prevents disruptive state resets.
- Improves operator efficiency.

# Replace History Entries

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | medium | Use `replace` for high-frequency query/filter updates | replace, history, filters, search |

Use `replace: true` for interactions that should not create many history entries.

## Agent Directives

- Trigger: frequent query/filter typing updates.
- Must: use `replace: true` for high-frequency state changes.
- Must Not: flood history stack with near-identical states.
- Auto: keep back-button behavior clean for operators.

## Bad Example

```ts
router.get('/users', { search })
```

## Good Example

```ts
router.get('/users', { search }, {
  replace: true,
  preserveState: true,
})
```

## Why

- Keeps browser history clean during frequent filter changes.
- Improves back-button behavior.

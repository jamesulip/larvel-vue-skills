# Programmatic Navigation

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Use Inertia router methods for programmatic visits | router, programmatic, visit, get, post |

Use `router.get/post/...` for programmatic transitions.

## Agent Directives

- Trigger: non-link based navigation (buttons, handlers, effects).
- Must: use Inertia `router` visit methods.
- Must Not: navigate with `window.location` for normal app flow.
- Auto: include `preserveScroll`/`preserveState` when workflow continuity is needed.

## Bad Example

```ts
window.location.href = '/users'
```

## Good Example

```ts
import { router } from '@inertiajs/vue3'

router.get('/users', {}, { preserveScroll: true })
```

## Why

- Keeps transitions within Inertia lifecycle.
- Supports visit options and events.

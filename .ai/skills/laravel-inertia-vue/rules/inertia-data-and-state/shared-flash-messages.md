# Shared Flash Messages

| section | priority | description | keywords |
| --- | --- | --- | --- |
| shared-data | high | Render flash success/error from shared props after redirects | flash, messages, redirect, feedback |

Use server-shared flash props for one-time feedback.

## Agent Directives

- Trigger: redirect-result feedback after create/update/delete.
- Must: read flash from shared Inertia props.
- Must Not: persist flash through localStorage/sessionStorage hacks.
- Auto: render flash in persistent shell feedback region.

## Bad Example

```ts
localStorage.setItem('toast', 'Saved')
```

## Good Example

```ts
import { computed } from 'vue'
import { usePage } from '@inertiajs/vue3'

const page = usePage<{ flash?: { success?: string; error?: string } }>()
const success = computed(() => page.props.flash?.success)
```

## Why

- Matches redirect lifecycle semantics.
- Avoids client-side message persistence hacks.

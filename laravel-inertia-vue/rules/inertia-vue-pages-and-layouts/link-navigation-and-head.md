# Link Navigation and Page Head

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Use Inertia Link for navigation and Head for title/meta | Link, Head, title, meta, scroll, events |

UI interaction rules:

- Use `Link` for internal navigation.
- Use `Head` for title/meta updates.
- Preserve scroll where workflow requires continuity.
- Use Inertia events for navigation-bound UI behavior.

## Bad Example

```vue
<script setup>
document.title = 'Users'
</script>

<template>
  <a href="/users">Users</a>
</template>
```

## Good Example

```vue
<script setup lang="ts">
import { Head, Link, router } from '@inertiajs/vue3'

const applyFilters = () => {
  router.get('/users', {}, { preserveScroll: true })
}
</script>

<template>
  <Head title="Users" />
  <Link href="/users/create">Create User</Link>
  <button @click="applyFilters">Refresh</button>
</template>
```

## Why

- Guarantees SPA navigation semantics.
- Keeps page metadata consistent and SSR-friendly.
- Prevents full reload regressions.

# Persistent App Shell

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | critical | Render dashboard pages inside persistent app shell | app-layout, sidebar, header, slot, dashboard |

Always generate authenticated pages inside a persistent shell containing:

- `AppLayout`
- Sidebar
- Header
- Content slot

No standalone page structure for dashboard routes.

## Bad Example

```vue
<template>
  <main>
    <h1>Users</h1>
    <UsersTable />
  </main>
</template>
```

## Good Example

```vue
<script setup lang="ts">
import AppLayout from '@/Layouts/AppLayout.vue'
</script>

<template>
  <AppLayout>
    <template #sidebar><SidebarNav /></template>
    <template #header><PageHeader title="Users" /></template>
    <UsersTable />
  </AppLayout>
</template>
```

## Why

- Preserves workspace context across page visits.
- Prevents shell remount jank in admin workflows.
- Standardizes UX and component composition.

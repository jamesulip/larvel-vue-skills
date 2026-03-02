# Page Default Layout

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Apply default app layout for authenticated pages | default-layout, app-shell, page-layout |

Ensure dashboard pages resolve to `AppLayout` by default.

## Agent Directives

- Trigger: creating new authenticated dashboard pages.
- Must: mount page inside `AppLayout` by default.
- Must Not: leave authenticated pages without shell wrapping.
- Auto: reserve shell-less pages for guest/auth screens only.

## Bad Example

```vue
<template>
  <section>Dashboard</section>
</template>
```

## Good Example

```vue
<script setup lang="ts">
import AppLayout from '@/Layouts/AppLayout.vue'
</script>

<template>
  <AppLayout>
    <section>Dashboard</section>
  </AppLayout>
</template>
```

## Why

- Guarantees shell consistency.
- Reduces one-off page layout divergence.

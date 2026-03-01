# Page Head Management

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Manage title/meta via Inertia `Head` component | head, title, meta, seo |

Use `Head` in every page to set title/meta values.

## Agent Directives

- Trigger: any page component generation.
- Must: set page title using Inertia `Head`.
- Must Not: mutate `document.title` directly as default pattern.
- Auto: include `Head` even for simple index pages.

## Bad Example

```ts
document.title = 'Users'
```

## Good Example

```vue
<script setup lang="ts">
import { Head } from '@inertiajs/vue3'
</script>

<template>
  <Head title="Users" />
</template>
```

## Why

- Keeps metadata declarative and consistent.
- Works with SSR-oriented setups.

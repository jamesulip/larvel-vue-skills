# Page Component Structure

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Keep page components focused on props, actions, and rendering | page, structure, props, composition-api |

A page should define typed props, local UI state, and Inertia actions only.

## Agent Directives

- Trigger: generating or refactoring page-level components.
- Must: keep page focused on props, UI composition, and Inertia interactions.
- Must Not: embed custom API orchestration or duplicated store sync.
- Auto: define typed props up front.

## Bad Example

```ts
// large page doing custom API orchestration + global store sync
```

## Good Example

```vue
<script setup lang="ts">
import { Head } from '@inertiajs/vue3'

defineProps<{ users: Array<{ id: number; name: string }> }>()
</script>

<template>
  <Head title="Users" />
  <UsersTable :rows="users" />
</template>
```

## Why

- Improves readability and reuse.
- Keeps server-driven contract explicit.

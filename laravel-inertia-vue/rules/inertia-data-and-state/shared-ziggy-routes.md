# Shared Ziggy Routes

| section | priority | description | keywords |
| --- | --- | --- | --- |
| shared-data | medium | Use Ziggy route helpers instead of hardcoded URL strings | ziggy, route, named-routes, url-generation |

Prefer named-route generation for internal links.

## Agent Directives

- Trigger: generating links/actions to server routes.
- Must: prefer named route helpers (Ziggy/Wayfinder when available).
- Must Not: hardcode route strings where named routes exist.
- Auto: pass route params explicitly for resource actions.

## Bad Example

```vue
<Link href="/users/12/edit">Edit</Link>
```

## Good Example

```vue
<script setup lang="ts">
import { Link } from '@inertiajs/vue3'
</script>

<template>
  <Link :href="route('users.edit', user.id)">Edit</Link>
</template>
```

## Why

- Reduces hardcoded URL drift.
- Keeps frontend aligned with server route names.

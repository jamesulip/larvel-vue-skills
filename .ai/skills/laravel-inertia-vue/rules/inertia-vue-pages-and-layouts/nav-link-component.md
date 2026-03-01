# Navigation Link Component

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | critical | Use Inertia `Link` for all internal navigation | Link, navigation, internal, spa |

Use `Link` for internal app routes.

## Agent Directives

- Trigger: rendering internal navigation elements.
- Must: use Inertia `Link` for internal URLs.
- Must Not: use plain anchors for internal route transitions.
- Auto: preserve Inertia SPA semantics for page transitions.

## Bad Example

```vue
<a href="/users">Users</a>
```

## Good Example

```vue
<script setup lang="ts">
import { Link } from '@inertiajs/vue3'
</script>

<template>
  <Link href="/users">Users</Link>
</template>
```

## Why

- Preserves Inertia SPA navigation behavior.
- Avoids full page reloads.

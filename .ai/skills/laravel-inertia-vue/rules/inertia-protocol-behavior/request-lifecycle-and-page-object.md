# Request Lifecycle and Page Object

| section | priority | description | keywords |
| --- | --- | --- | --- |
| protocol | critical | Enforce Inertia request lifecycle and page object contract | lifecycle, page-object, xhr, html, version |

Treat Inertia as protocol transport:

- First response is HTML bootstrap.
- Subsequent internal visits are XHR Inertia responses.
- Page payload is server-owned (`component`, `props`, `url`, `version`).
- Client swaps page component; it does not fetch page JSON manually.

## Bad Example

```ts
const page = await fetch('/dashboard').then(r => r.json())
currentComponent.value = page.component
```

## Good Example

```vue
<script setup lang="ts">
import { Link, usePage } from '@inertiajs/vue3'

const page = usePage()
</script>

<template>
  <Link href="/dashboard">Dashboard</Link>
  <h1>{{ page.component }}</h1>
</template>
```

## Why

- Maintains Inertia protocol guarantees.
- Avoids broken behavior between HTML bootstrap and XHR visits.
- Keeps server authoritative for page object shape.

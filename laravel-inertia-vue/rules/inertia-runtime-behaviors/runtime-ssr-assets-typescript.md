# SSR, Asset Versioning, and TypeScript Compatibility

| section | priority | description | keywords |
| --- | --- | --- | --- |
| runtime-ui | medium | Keep generated code compatible with SSR, asset versioning, and TypeScript workflows | ssr, asset-versioning, code-splitting, typescript, testing |

Generate runtime-safe Vue/Inertia code that avoids browser-only assumptions and supports typed props.

## Bad Example

```ts
const width = window.innerWidth
const title = (usePage() as any).props.pageTitle
```

## Good Example

```vue
<script setup lang="ts">
import { computed } from 'vue'
import { usePage } from '@inertiajs/vue3'

interface PageProps {
  pageTitle?: string
}

const page = usePage<PageProps>()
const title = computed(() => page.props.pageTitle ?? 'Dashboard')
</script>

<template>
  <h1>{{ title }}</h1>
</template>
```

## Why

- Improves correctness across SSR and hydration.
- Reduces runtime issues after asset/version refresh.
- Maintains type-safe page contracts.

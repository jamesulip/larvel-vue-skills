# Server-Driven Navigation and Redirects

| section | priority | description | keywords |
| --- | --- | --- | --- |
| protocol | critical | Keep navigation and redirects server-driven through Inertia visits | redirects, manual-visits, router, link, server-routes |

Navigation rules:

- Use `Link` and Inertia router methods for internal visits.
- Mutations resolve through server redirects.
- Controllers return pages, not ad-hoc JSON for page rendering.
- Never emulate redirects with manual `window.location` for normal flows.

## Bad Example

```ts
await axios.post('/users', payload)
window.location.href = '/users'
```

## Good Example

```vue
<script setup lang="ts">
import { useForm } from '@inertiajs/vue3'

const form = useForm({ name: '' })

const submit = () => {
  form.post('/users')
}
</script>

<template>
  <form @submit.prevent="submit">
    <input v-model="form.name" />
    <button :disabled="form.processing" type="submit">Save</button>
  </form>
</template>
```

## Why

- Redirect semantics are part of Inertia’s contract.
- Reduces client-side routing drift and stale state.
- Keeps mutation outcomes consistent across pages.

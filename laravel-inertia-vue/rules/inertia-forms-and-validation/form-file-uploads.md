# Form File Uploads

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | critical | Handle file uploads through `useForm` without custom request stacks | file, upload, multipart, useForm |

Use file inputs with `useForm`; submit with normal Inertia form methods.

## Agent Directives

- Trigger: forms with file/image/document fields.
- Must: keep upload submission through Inertia `useForm` methods.
- Must Not: switch to manual fetch/axios upload stack for standard flows.
- Auto: surface file field validation from `form.errors`.

## Bad Example

```ts
const fd = new FormData()
fd.append('avatar', file)
await fetch('/profile', { method: 'POST', body: fd })
```

## Good Example

```vue
<script setup lang="ts">
import { useForm } from '@inertiajs/vue3'
const form = useForm<{ avatar: File | null }>({ avatar: null })
</script>

<template>
  <input type="file" @change="form.avatar = ($event.target as HTMLInputElement).files?.[0] ?? null" />
  <button @click="form.post('/profile')" :disabled="form.processing">Upload</button>
</template>
```

## Why

- Keeps uploads integrated with validation/error handling.
- Avoids duplicate networking logic.

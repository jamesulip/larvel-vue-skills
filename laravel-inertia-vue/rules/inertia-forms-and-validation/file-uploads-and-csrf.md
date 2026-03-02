# File Uploads and CSRF Handling

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | critical | Support file uploads with useForm and rely on Laravel CSRF/session defaults | file-uploads, csrf, session-auth, security |

File uploads should use Inertia form submission; do not manually attach CSRF tokens for standard Laravel setups.

## Bad Example

```ts
const fd = new FormData()
fd.append('avatar', file)

await fetch('/profile', {
  method: 'POST',
  headers: { 'X-CSRF-TOKEN': token },
  body: fd,
})
```

## Good Example

```vue
<script setup lang="ts">
import { useForm } from '@inertiajs/vue3'

const form = useForm<{ avatar: File | null }>({
  avatar: null,
})

const submit = () => {
  form.post('/profile')
}
</script>

<template>
  <form @submit.prevent="submit">
    <input type="file" @change="form.avatar = ($event.target as HTMLInputElement).files?.[0] ?? null" />
    <p v-if="form.errors.avatar">{{ form.errors.avatar }}</p>
    <button type="submit" :disabled="form.processing">Upload</button>
  </form>
</template>
```

## Why

- Inertia/Laravel already provides request and CSRF handling.
- Reduces security mistakes in custom request code.
- Keeps uploads aligned with normal validation/redirect flow.

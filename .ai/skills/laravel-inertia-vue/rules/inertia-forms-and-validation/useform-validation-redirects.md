# useForm, Validation, and Redirect Flow

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | critical | Use Inertia useForm with server validation and redirect semantics | useForm, validation, redirects, errors, processing |

Mutations must use `useForm`; validation errors are server-provided and displayed from `form.errors`.

## Bad Example

```ts
const submit = async () => {
  try {
    await axios.post('/users', payload)
  } catch (error: any) {
    localErrors.value = error.response.data.errors
  }
}
```

## Good Example

```vue
<script setup lang="ts">
import { useForm } from '@inertiajs/vue3'

const form = useForm({
  name: '',
  email: '',
})

const submit = () => {
  form.post('/users')
}
</script>

<template>
  <form @submit.prevent="submit">
    <input v-model="form.name" name="name" />
    <p v-if="form.errors.name">{{ form.errors.name }}</p>

    <input v-model="form.email" type="email" name="email" />
    <p v-if="form.errors.email">{{ form.errors.email }}</p>

    <button type="submit" :disabled="form.processing">Save</button>
  </form>
</template>
```

## Why

- Matches Inertia’s validation lifecycle.
- Removes ad-hoc 422 parsing.
- Keeps mutation UX consistent across forms.

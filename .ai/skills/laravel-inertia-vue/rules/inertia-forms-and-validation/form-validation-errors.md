# Validation Error Rendering

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | critical | Render field errors from `form.errors` and server props | validation, errors, form.errors, redirects |

Display validation errors directly from Inertia form state and avoid ad-hoc error maps.

## Agent Directives

- Trigger: adding or refactoring field-level validation UI.
- Must: render errors from `form.errors` (or shared Inertia errors).
- Must Not: parse manual 422 payloads as primary behavior.
- Auto: place error text adjacent to the relevant field.

## Bad Example

```ts
catch (e) {
  errors.value = e.response.data.errors
}
```

## Good Example

```vue
<script setup lang="ts">
import { useForm } from '@inertiajs/vue3'
const form = useForm({ name: '' })
</script>

<template>
  <input v-model="form.name" name="name" />
  <p v-if="form.errors.name">{{ form.errors.name }}</p>
</template>
```

## Why

- Follows Inertia redirect-based validation flow.
- Prevents 422-specific coupling.

# Form Progress Indicator

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | high | Show visible submission progress/loading state for forms | processing, loading, disabled, UX |

Always bind submit controls to `form.processing` and show pending state.

## Agent Directives

- Trigger: any asynchronous form submission UI.
- Must: disable submit while `form.processing` is true.
- Must Not: allow repeat submit clicks during request.
- Auto: include pending label (for example `Saving...`).

## Bad Example

```vue
<button @click="submit">Save</button>
```

## Good Example

```vue
<script setup lang="ts">
import { useForm } from '@inertiajs/vue3'
const form = useForm({ name: '' })
</script>

<template>
  <button :disabled="form.processing" @click="form.post('/users')">
    {{ form.processing ? 'Saving...' : 'Save' }}
  </button>
</template>
```

## Why

- Prevents duplicate submissions.
- Improves clarity during async operations.

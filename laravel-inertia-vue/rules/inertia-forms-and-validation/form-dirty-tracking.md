# Form Dirty Tracking

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | high | Track unsaved changes using Inertia form dirty state | dirty, isDirty, unsaved, guard |

Use `form.isDirty` to warn users before losing unsaved changes.

## Agent Directives

- Trigger: editable forms with navigation-away risk.
- Must: derive unsaved state from `form.isDirty`.
- Must Not: implement manual deep-diff tracking unless required.
- Auto: show a visible unsaved-changes hint when dirty.

## Bad Example

```ts
const dirty = JSON.stringify(form) !== JSON.stringify(original)
```

## Good Example

```vue
<script setup lang="ts">
import { computed } from 'vue'
import { useForm } from '@inertiajs/vue3'

const form = useForm({ name: '' })
const hasUnsavedChanges = computed(() => form.isDirty)
</script>

<template>
  <p v-if="hasUnsavedChanges">You have unsaved changes.</p>
</template>
```

## Why

- Reduces accidental data loss.
- Reuses built-in form state instead of custom diff logic.

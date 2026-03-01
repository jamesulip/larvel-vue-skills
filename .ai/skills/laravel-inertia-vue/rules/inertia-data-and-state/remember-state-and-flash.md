# Remembered State and Flash Messages

| section | priority | description | keywords |
| --- | --- | --- | --- |
| data-lifecycle | high | Preserve filter state and show one-time flash data correctly | remembering-state, flash-data, preserveState, preserveScroll |

Remember filter/UI state for workflow continuity and render flash messages from shared props.

## Bad Example

```vue
<script setup lang="ts">
const search = ref('')

watch(search, () => {
  router.get('/users', { search: search.value })
})

// resets on revisit, no flash rendering
</script>
```

## Good Example

```vue
<script setup lang="ts">
import { computed, ref } from 'vue'
import { router, usePage } from '@inertiajs/vue3'

const page = usePage<{ flash?: { success?: string; error?: string } }>()
const flashSuccess = computed(() => page.props.flash?.success)
const search = ref('')

const applySearch = () => {
  router.get('/users', { search: search.value }, {
    preserveState: true,
    preserveScroll: true,
    replace: true,
  })
}
</script>

<template>
  <p v-if="flashSuccess" class="text-green-600">{{ flashSuccess }}</p>
  <input v-model="search" @input="applySearch" />
</template>
```

## Why

- Preserves operator context in dashboard workflows.
- Uses Inertia flash model instead of ad-hoc toast transport.
- Prevents jarring resets on list navigation.

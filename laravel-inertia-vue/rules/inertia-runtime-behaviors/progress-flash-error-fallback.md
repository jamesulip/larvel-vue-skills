# Progress, Flash, and Error Fallback

| section | priority | description | keywords |
| --- | --- | --- | --- |
| runtime-ui | high | Include progress indication, flash display, and error fallback in app shell | progress-indicator, flash, error-handling, events |

Every generated page flow should include runtime feedback surfaces in the persistent layout.

## Bad Example

```vue
<template>
  <main><slot /></main>
</template>
```

## Good Example

```vue
<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue'
import { router, usePage } from '@inertiajs/vue3'

const loading = ref(false)
const page = usePage<{ flash?: { success?: string; error?: string } }>()
const flash = computed(() => page.props.flash)

const offStart = router.on('start', () => (loading.value = true))
const offFinish = router.on('finish', () => (loading.value = false))

onMounted(() => {
  void offStart
  void offFinish
})

onUnmounted(() => {
  offStart()
  offFinish()
})
</script>

<template>
  <div v-if="loading" class="h-1 bg-blue-500" />
  <p v-if="flash?.success">{{ flash.success }}</p>
  <p v-if="flash?.error">{{ flash.error }}</p>
  <slot />
</template>
```

## Why

- Gives immediate navigation feedback.
- Makes redirect outcomes visible.
- Improves resilience during runtime exceptions.

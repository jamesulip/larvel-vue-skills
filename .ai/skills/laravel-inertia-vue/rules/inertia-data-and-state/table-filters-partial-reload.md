# Table Filters with Partial Reload

| section | priority | description | keywords |
| --- | --- | --- | --- |
| data-lifecycle | critical | Implement table filter/search/pagination via partial reload | tables, filters, search, pagination, partial-reloads, performance |

For dashboard tables, prefer same-page partial reload for filter/search/sort/page changes.

## Bad Example

```ts
const rows = ref([])

const refresh = async (q: string) => {
  rows.value = await axios.get('/api/users', { params: { q } }).then(r => r.data)
}
```

## Good Example

```vue
<script setup lang="ts">
import { ref } from 'vue'
import { router } from '@inertiajs/vue3'

const filters = ref({ search: '', page: 1 })

const applyFilters = () => {
  router.get('/users', filters.value, {
    only: ['users', 'filters', 'meta'],
    preserveState: true,
    preserveScroll: true,
    replace: true,
  })
}
</script>

<template>
  <input v-model="filters.search" @input="applyFilters" placeholder="Search users" />
</template>
```

## Why

- Reduces payload for table-heavy screens.
- Keeps filters and pagination synchronized with server state.
- Avoids stale local copies and API drift.

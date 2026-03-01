# Global Constraints

| section | priority | description | keywords |
| --- | --- | --- | --- |
| global | critical | Non-negotiable constraints for all Laravel + Inertia + Vue generation | vue3, composition-api, inertia, server-routing, no-vue-router, no-axios |

All generated output must follow these constraints:

- Vue 3 Composition API with `<script setup>` only.
- No Vue Router.
- No axios/fetch for page data.
- No Pinia/Vuex duplication of server props.
- Server routing is source of truth.
- Backend controllers already exist; do not generate Laravel controller logic.

## Bad Example

```ts
import axios from 'axios'
import { useRouter } from 'vue-router'

const router = useRouter()
const users = await axios.get('/api/users')
router.push('/users')
```

## Good Example

```vue
<script setup lang="ts">
import { Link, usePage } from '@inertiajs/vue3'

const page = usePage<{ users: Array<{ id: number; name: string }> }>()
</script>

<template>
  <Link href="/users">Users</Link>
  <ul>
    <li v-for="user in page.props.users" :key="user.id">{{ user.name }}</li>
  </ul>
</template>
```

## Why

- Keeps architecture protocol-correct and consistent.
- Prevents retrieval drift into SPA-router/API patterns.
- Preserves server-driven page orchestration.

# Shared Auth User Data

| section | priority | description | keywords |
| --- | --- | --- | --- |
| shared-data | critical | Access authenticated user data through Inertia shared props | auth, user, authentication, shared, middleware, HandleInertiaRequests |

Access authenticated user state from shared Inertia props configured in Laravel middleware. Do not fetch auth user separately on each page.

## Agent Directives

- Trigger: auth-aware UI (menus, guards, role checks).
- Must: consume `auth.user` from shared props.
- Must Not: fetch `/api/user` per page.
- Auto: expose small typed auth helper/composable where repeated.

## Bad Example

```vue
<script setup lang="ts">
import { onMounted, ref } from 'vue'

const user = ref<any>(null)

onMounted(async () => {
  user.value = await fetch('/api/user').then(r => r.json())
})
</script>

<template>
  <div v-if="user">Welcome {{ user.name }}</div>
</template>
```

## Good Example

```php
<?php
// app/Http/Middleware/HandleInertiaRequests.php

namespace App\Http\Middleware;

use Illuminate\Http\Request;
use Inertia\Middleware;

class HandleInertiaRequests extends Middleware
{
    public function share(Request $request): array
    {
        return array_merge(parent::share($request), [
            'auth' => [
                'user' => $request->user() ? [
                    'id' => $request->user()->id,
                    'name' => $request->user()->name,
                    'email' => $request->user()->email,
                ] : null,
            ],
        ]);
    }
}
```

```vue
<script setup lang="ts">
import { computed } from 'vue'
import { usePage } from '@inertiajs/vue3'

interface User {
  id: number
  name: string
  email: string
}

interface PageProps {
  auth: { user: User | null }
}

const page = usePage<PageProps>()
const user = computed(() => page.props.auth.user)
const isAuthenticated = computed(() => !!user.value)
</script>

<template>
  <div v-if="isAuthenticated">Welcome {{ user?.name }}</div>
</template>
```

## Why

- Single source of truth for auth state.
- No extra API request overhead.
- Works consistently with SSR and Inertia visits.

# useForm Hook Pattern

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | high | Wrap repeated form behavior in composables while keeping Inertia semantics | composable, hook, useForm, reuse |

Use a composable to standardize repeated form logic, but keep the underlying primitive as `useForm`.

## Agent Directives

- Trigger: repeated create/edit form workflows across pages.
- Must: keep `useForm` inside composables and expose submit helpers.
- Must Not: replace with plain reactive objects for mutation transport.
- Auto: provide both create and update submit actions when resource supports both.

## Bad Example

```ts
export function useUserForm() {
  return reactive({ name: '', email: '' })
}
```

## Good Example

```ts
import { useForm } from '@inertiajs/vue3'

export function useUserForm(initial?: { name?: string; email?: string }) {
  const form = useForm({ name: initial?.name ?? '', email: initial?.email ?? '' })
  const submitCreate = () => form.post('/users')
  const submitUpdate = (id: number) => form.put(`/users/${id}`)
  return { form, submitCreate, submitUpdate }
}
```

## Why

- Improves consistency across create/edit pages.
- Preserves Inertia-native behavior.

# useForm Basic Usage

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | critical | Use `useForm` as the default form primitive for mutations | useForm, form, submit, processing, inertia |

Always initialize forms with `useForm` and submit via `form.post/put/patch/delete`.

## Agent Directives

- Trigger: creating or editing CRUD forms.
- Must: initialize with `useForm` and submit through Inertia form methods.
- Must Not: use axios/fetch for page mutations.
- Auto: bind submit disabled/loading to `form.processing`.

## Bad Example

```ts
const submit = async () => {
  await axios.post('/users', state)
}
```

## Good Example

```vue
<script setup lang="ts">
import { useForm } from '@inertiajs/vue3'

const form = useForm({ name: '', email: '' })
const submit = () => form.post('/users')
</script>
```

## Why

- Aligns with Inertia validation and redirect lifecycle.
- Provides built-in processing/error states.

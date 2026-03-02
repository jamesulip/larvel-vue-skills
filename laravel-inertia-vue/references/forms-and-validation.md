# Forms and Validation

## useForm Baseline
Use `useForm` for create/edit flows and map server validation errors directly.

```ts
const form = useForm({
  name: "",
  status: "pending",
  notes: "",
});
```

Submit with explicit lifecycle handlers:

```ts
form.post(route("projects.store"), {
  preserveScroll: true,
  onError: () => focusFirstError(),
  onSuccess: () => form.reset("notes"),
});
```

## Validation Rules
- Keep Laravel validation rules as source of truth.
- Render errors from `form.errors`.
- Do not create parallel frontend-only rule engines unless explicitly required.

## Submit Safety
- Use `form.processing` to disable submit buttons.
- Show loading indicators while processing.
- Prevent double submission until request finishes.

## Edit Flow
- Use `form.put`/`form.patch` for updates.
- Keep cancel flow explicit and confirm when form is dirty.

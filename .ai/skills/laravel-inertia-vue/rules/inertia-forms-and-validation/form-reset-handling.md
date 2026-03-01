# Form Reset Handling

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | medium | Reset form data intentionally after success or cancel actions | reset, defaults, clearErrors, post-success |

Reset fields only when workflow requires it and keep error/reset behavior explicit.

## Agent Directives

- Trigger: submit success flows and cancel actions.
- Must: reset only in success/cancel handlers with explicit intent.
- Must Not: reset immediately after submit before server response.
- Auto: clear errors when reset is intentional.

## Bad Example

```ts
form.post('/users')
form.reset()
```

## Good Example

```ts
const submit = () => {
  form.post('/users', {
    onSuccess: () => {
      form.reset()
      form.clearErrors()
    },
  })
}
```

## Why

- Avoids erasing user input on failed validation.
- Keeps post-success UX predictable.

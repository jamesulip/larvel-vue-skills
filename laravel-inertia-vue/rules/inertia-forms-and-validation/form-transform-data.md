# Form Data Transform

| section | priority | description | keywords |
| --- | --- | --- | --- |
| forms-validation | medium | Transform submission payload with `form.transform` before sending | transform, payload, normalize, submit |

Use `form.transform` to normalize request payloads without mutating template bindings.

## Agent Directives

- Trigger: UI value format differs from API payload format.
- Must: normalize payload via `form.transform` immediately before submit.
- Must Not: mutate bound input state solely for transport formatting.
- Auto: keep display-friendly value and transport-friendly value separated.

## Bad Example

```ts
form.phone = form.phone.replace(/\D/g, '')
form.post('/contacts')
```

## Good Example

```ts
form
  .transform((data) => ({
    ...data,
    phone: data.phone.replace(/\D/g, ''),
  }))
  .post('/contacts')
```

## Why

- Keeps display state separate from transport payload.
- Centralizes request normalization.

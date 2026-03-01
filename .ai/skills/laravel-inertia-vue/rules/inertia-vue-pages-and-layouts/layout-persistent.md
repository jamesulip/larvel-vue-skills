# Persistent Layout

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | critical | Keep dashboard layout mounted across Inertia visits | layout, persistent, shell, sidebar, header |

Use a persistent app shell for authenticated areas.

## Agent Directives

- Trigger: authenticated dashboard/admin page generation.
- Must: wrap content in persistent `AppLayout` shell.
- Must Not: output standalone full-page structure for internal routes.
- Auto: include sidebar, header, and content region.

## Bad Example

```vue
<template>
  <main><slot /></main>
</template>
```

## Good Example

```vue
<template>
  <AppLayout>
    <slot />
  </AppLayout>
</template>
```

## Why

- Maintains workflow context between page visits.
- Prevents repetitive shell re-rendering.

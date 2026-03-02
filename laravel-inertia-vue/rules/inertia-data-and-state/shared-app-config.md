# Shared App Config

| section | priority | description | keywords |
| --- | --- | --- | --- |
| shared-data | high | Share global app config via Inertia middleware, not per-page duplication | config, shared, appName, environment |

Expose small, stable app config from shared props.

## Agent Directives

- Trigger: global app info needed across multiple pages/components.
- Must: source config from shared props middleware.
- Must Not: duplicate env/config reads in many components.
- Auto: keep shared config small and stable.

## Bad Example

```ts
const appName = import.meta.env.VITE_APP_NAME
// repeated in many components
```

## Good Example

```php
// HandleInertiaRequests::share
'app' => [
  'name' => config('app.name'),
  'env' => app()->environment(),
],
```

```ts
const page = usePage<{ app: { name: string; env: string } }>()
```

## Why

- Centralizes globally-used configuration.
- Prevents prop drilling and duplication.

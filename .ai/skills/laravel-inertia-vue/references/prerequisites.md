# Prerequisites

## Verify Existing Setup
Check before installing:

- `composer.json` contains `inertiajs/inertia-laravel`
- `package.json` contains `@inertiajs/vue3`
- `resources/js/app.ts` or `resources/js/app.js` uses `createInertiaApp`
- `app/Http/Middleware/HandleInertiaRequests.php` exists and is registered

If all are present, do not reinstall.

## Install Inertia (If Missing)

Backend:

```bash
composer require inertiajs/inertia-laravel
php artisan inertia:middleware
```

Frontend:

```bash
npm install @inertiajs/vue3
```

## App Bootstrap Baseline

Use a single Inertia app entry (`resources/js/app.ts`):

```ts
import { createApp, h } from "vue";
import { createInertiaApp } from "@inertiajs/vue3";
import { resolvePageComponent } from "laravel-vite-plugin/inertia-helpers";

createInertiaApp({
  resolve: (name) =>
    resolvePageComponent(`./pages/${name}.vue`, import.meta.glob("./pages/**/*.vue")),
  setup({ el, App, props, plugin }) {
    createApp({ render: () => h(App, props) }).use(plugin).mount(el);
  },
});
```

## Server Render Baseline
Controller actions return Inertia responses:

```php
return Inertia::render('Projects/Index', [
    'projects' => $projects,
]);
```

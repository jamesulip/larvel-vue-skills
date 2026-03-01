---
name: laravel-inertia-vue
description: Implement Laravel + Inertia + Vue application patterns for setup, page/layout wiring, shared props, navigation state, and server-validated forms.
metadata:
  tags:
    - laravel
    - inertia
    - vue
    - spa
    - crud
    - forms
---

# Laravel Inertia Vue

## Overview

Use this skill to apply stable Inertia.js patterns in Laravel back-office SPAs.
Favor deterministic page wiring, server-driven data flow, and predictable navigation/form behavior.

## When To Use

- Work on Inertia controllers returning `Inertia::render(...)`.
- Build or refactor `resources/js/app.ts` and page layout wiring.
- Implement filters, pagination, and preserved state flows.
- Implement create/edit forms using `useForm` with Laravel validation.

## Quick Start

1. Read [references/prerequisites.md](references/prerequisites.md) to verify or install Inertia.
2. Read [references/page-layouts.md](references/page-layouts.md) when creating or refactoring pages/layouts.
3. Read [references/navigation-and-state.md](references/navigation-and-state.md) for search, filters, pagination, and preserved state.
4. Read [references/forms-and-validation.md](references/forms-and-validation.md) for create/edit forms and Laravel validation mapping.
5. Read [references/shared-data.md](references/shared-data.md) for shared props, flash messages, and authorization context.

## Non-Negotiables

- Keep Laravel validation as the only source of truth for form errors.
- Keep Inertia pages focused on rendering and interaction; keep domain rules in Laravel.
- Preserve state and scroll on workflow-heavy navigation interactions.
- Use route names and structured params rather than hardcoded URL strings where possible.
- Use Vue 3 Composition API with `<script setup>` unless project constraints require otherwise.

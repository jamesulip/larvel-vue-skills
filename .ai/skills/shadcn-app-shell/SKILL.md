---
name: shadcn-app-shell
description: "Build and enforce an authenticated Laravel + Inertia + Vue internal application shell with persistent layout, workflow-first navigation, standardized data tables/forms, feedback patterns, and production lifecycle UX. Use when scaffolding or refactoring back-office SPA dashboards, AppLayout/Sidebar/Topbar/PageContainer structure, CRUD list/form modules, keyboard shortcuts, and operator-focused workflow screens. Keywords: vue, laravel, inertia, shadcn-vue, dashboard, app-shell."
---

# Shadcn App Shell

## Overview

Use this skill to build ERP-style internal dashboards where pages render inside a persistent shell and operators prioritize speed, clarity, and repeatability.
Prefer Vue 3 Composition API with `<script setup>` and TypeScript unless the project explicitly requires a different style.

## Quick Start

1. Apply [shadcn-vue-prerequisites.md](shadcn-vue-prerequisites.md) before generating shell components.
2. Apply [Laravel Inertia Vue skill](../laravel-inertia-vue/SKILL.md) for Inertia routing, props, and form conventions.
3. Read [app-shell-architect.md](app-shell-architect.md) before generating any page layout.
4. Read [workspace-navigation.md](workspace-navigation.md) when defining routes, breadcrumbs, preserved state, and keyboard shortcuts.
5. Read [app-data-table-standard.md](app-data-table-standard.md) for any list or index screen.
6. Read [inertia-crud-form-standard.md](inertia-crud-form-standard.md) for create/edit forms.
7. Read [system-feedback-standard.md](system-feedback-standard.md) for toasts, loading states, and empty states.
8. Read [production-workflow-awareness.md](production-workflow-awareness.md) for printing and work-unit lifecycle interfaces.
9. Apply [final-behavior-rule.md](final-behavior-rule.md) to all generated UI.

## Non-Negotiables

- Keep `AppLayout` mounted across Inertia visits.
- Keep navigation and workspace context persistent.
- Standardize behavior across modules instead of creating one-off patterns.
- If `shadcn-vue` is not initialized, initialize it before generating components.
- Apply `laravel-inertia-vue` conventions for page contracts, navigation state, and forms.
- Optimize for operator throughput, not marketing presentation.

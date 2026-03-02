---
name: laravel-inertia-vue
description: Coordinate modular Laravel + Inertia + Vue skills with deterministic app-shell enforcement for internal dashboard pages using shadcn-vue primitives.
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

Use this skill as the coordinator for modular Inertia behavior skills.
For internal dashboard UI generation and refactors, enforce a deterministic application-shell contract via `shadcn-app-shell`.
Load focused subsystem skills based on task intent to avoid monolithic retrieval noise.

## When To Use

- You are generating or refactoring Vue 3 + Inertia admin/app-shell code.
- You need to select protocol, pages/layouts, data/state, forms, or runtime behavior rules.
- You need deterministic internal dashboard UI conventions powered by shadcn-vue primitives.

## Skill Pack

1. [inertia-protocol-behavior/SKILL.md](inertia-protocol-behavior/SKILL.md)
2. [inertia-vue-pages-and-layouts/SKILL.md](inertia-vue-pages-and-layouts/SKILL.md)
3. [inertia-data-and-state/SKILL.md](inertia-data-and-state/SKILL.md)
4. [inertia-forms-and-validation/SKILL.md](inertia-forms-and-validation/SKILL.md)
5. [inertia-runtime-behaviors/SKILL.md](inertia-runtime-behaviors/SKILL.md)
6. [rules/global/global-constraints.md](rules/global/global-constraints.md)
7. [../shadcn-app-shell/SKILL.md](../shadcn-app-shell/SKILL.md) (required for internal dashboard application-shell UI contract)

## Non-Negotiables

- Vue 3 Composition API only (`<script setup>`).
- No Vue Router.
- No axios/fetch for page data.
- No client stores duplicating server props.
- Server routing is source of truth.
- Do not generate Laravel controller logic.
- Internal dashboard pages must conform to the deterministic app-shell contract and use shadcn-vue primitives.

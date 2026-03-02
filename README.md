# Laravel App Skills

Monorepo of reusable skill packs for Laravel + Inertia + Vue application work.

## Included skill packs

### 1) Laravel Inertia Vue
Rule-first skill pack for Laravel + Inertia + Vue 3 patterns with deterministic internal dashboard app-shell enforcement.

- Path: `laravel-inertia-vue/`
- Entry: `laravel-inertia-vue/SKILL.md`
- Focus: deterministic dashboard app-shell conventions, page/layout patterns, shared props/state, forms/validation, Inertia protocol/runtime behavior

Suggested prompt:

> Use $laravel-inertia-vue to enforce a deterministic Laravel + Inertia + Vue internal dashboard app-shell contract with shadcn-vue primitives, plus robust pages, forms, navigation, shared props, and validation flows.

### 2) Shadcn App Shell
Skill pack for building a persistent Laravel + Inertia + Vue internal operations shell with shadcn-vue conventions.

- Path: `shadcn-app-shell/`
- Entry: `shadcn-app-shell/SKILL.md`
- Focus: authenticated app shell, navigation, data table/index behavior, CRUD form standards, system feedback/workflow

Suggested prompt:

> Use $shadcn-app-shell to scaffold an authenticated Laravel + Inertia + Vue application shell optimized for internal operations workflows.

## Repository structure

```text
laravel-app-skills/
├── laravel-inertia-vue/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   ├── inertia-*/
│   ├── references/
│   └── rules/
└── shadcn-app-shell/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── *.md standards
```

## Notes

- Each skill pack is versioned independently (see each package `CHANGELOG.md`).
- Each package contains its own prerequisites and usage details in its local `README.md`.

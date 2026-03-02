# Prerequisite - shadcn-vue setup

## Purpose
Ensure `shadcn-vue` is available before generating shell UI components.

## Detection Rule
- Check for `components.json` in the Vue app root.
- If `components.json` is missing, treat `shadcn-vue` as not initialized.

## Install Rule (when not initialized)
Run:

```bash
npx shadcn-vue@latest init
```

Use:
- `cssVariables: true`
- a stable style choice (`Default` or `New York`) that matches the existing project

## Component Add Rule
After initialization (or when already initialized), add missing components used by this shell:

```bash
npx shadcn-vue@latest add button badge avatar dropdown-menu breadcrumb separator sheet command dialog input table checkbox skeleton toast progress
```

If only one component is missing, add it individually:

```bash
npx shadcn-vue@latest add <component-name>
```

## Guardrails
- Do not regenerate or overwrite components that already exist unless the task explicitly asks for updates.
- Keep component usage consistent across modules by reusing the same primitives.

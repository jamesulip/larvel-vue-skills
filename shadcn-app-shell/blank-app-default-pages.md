# Blank App Default Pages Standard

## Purpose
Define the default page scaffold for a blank Laravel + Inertia + Vue app using this skill.

This is a starter profile: minimal, production-structured, and easy to extend.

## Canonical Page Contract
Every starter page must follow this structure:

```vue
<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue'
import PageContainer from '@/components/layout/PageContainer.vue'
import { Head } from '@inertiajs/vue3'

const breadcrumbs = [
  { title: 'Dashboard', href: '/dashboard' },
]
</script>

<template>
  <Head title="Dashboard" />

  <AppLayout :breadcrumbs="breadcrumbs">
    <PageContainer>
      <section class="space-y-4">
        <header class="flex flex-col gap-3 sm:flex-row sm:items-start sm:justify-between">
          <div class="space-y-1">
            <h1 class="text-xl font-semibold tracking-tight">Dashboard</h1>
            <p class="text-muted-foreground text-sm">Workspace summary and key actions.</p>
          </div>
          <div class="flex items-center gap-2">
            <!-- page actions -->
          </div>
        </header>

        <!-- page body -->
      </section>
    </PageContainer>
  </AppLayout>
</template>
```

Rules:
- Use `<Head>` for page title.
- Wrap page content in `<AppLayout :breadcrumbs="breadcrumbs">`.
- Wrap inner content with `<PageContainer>`.
- Use a shared header block pattern (title/description on left, actions on right).
- Keep `breadcrumbs` local to each page and pass as array objects: `{ title: string, href?: string }`.
- Apply [page-template-ui-consistency.md](page-template-ui-consistency.md) for all starter pages.

## Skill-Creator Execution Order
When generating starter pages, execute in this order:
1. Create `AppLayout.vue` and `PageContainer.vue` if missing.
2. Create `Dashboard.vue`.
3. Create `Users/Index.vue` using plain shadcn-vue table.
4. Create `Forms/UserFormDemo.vue`.
5. Create `Settings/Index.vue`.
6. Add shared feedback primitives (`EmptyState`, toast usage) required by starter pages.

## Starter File Tree (Lite)

```text
resources/js/
├─ layouts/
│  └─ AppLayout.vue
├─ pages/
│  ├─ Dashboard.vue
│  ├─ Users/
│  │  └─ Index.vue
│  ├─ Forms/
│  │  └─ UserFormDemo.vue
│  └─ Settings/
│     └─ Index.vue
└─ components/
   ├─ layout/
   │  └─ PageContainer.vue
   ├─ system/
   │  └─ EmptyState.vue
   └─ form/
      └─ FormSection.vue
```

## Required Starter Pages

### 1) Dashboard
- Title: `Dashboard`
- Show concise workspace context and key operator actions.
- Keep layout density high and scanning easy.

### 2) Users Listing
- Title: `Users`
- Use a plain shadcn-vue table (`components/ui/table`) as the default.
- Do not default to `DataTable.vue` for starter list pages.
- Include loading and empty states.

### 3) Form UI Demo
- Title: `User Form`
- Demonstrate sectioned form layout, validation rendering, dirty-check cancel, and submit loading state.

### 4) Settings
- Title: `Settings`
- Group settings by clear sections (profile, preferences, security/system).
- Keep controls straightforward and operational.

## Linear-Inspired (Light)
Use inspiration from Linear for structure only:
- Concise page titles.
- Clear workspace context.
- Tight, consistent spacing.
- Fast scan hierarchy with low visual noise.

Do not mimic Linear branding or visuals.

## Out of Scope for Starter
- Do not force advanced command-palette or power-user workflows on day one.
- Do not require every advanced table feature before initial scaffold is usable.
- Add advanced behaviors incrementally through the other standards in this folder.

## Output Acceptance Checklist
- All starter pages use `Head` + `AppLayout :breadcrumbs`.
- All starter pages use `PageContainer` and shared header hierarchy.
- `Users/Index.vue` uses `components/ui/table` primitives (not `DataTable.vue`).
- Form starter renders server validation errors and pending submit state.
- List starter renders loading and empty states.
- Settings starter is sectioned and operational (no marketing UI patterns).

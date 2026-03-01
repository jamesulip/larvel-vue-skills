# Skill 1 - app-shell-architect

## Purpose
Define the permanent application frame. Render pages inside the shell and never replace it during navigation.

## Required File
- `resources/js/layouts/AppLayout.vue`

## Required Shell Structure

```text
AppLayout
├─ Sidebar (persistent navigation)
├─ Topbar (context + actions)
└─ Content Workspace (page slot)
```

The shell must not unmount between Inertia page visits.

## Inertia Layout Rule
- Require every page to declare `AppLayout` as the layout.
- In `<script setup>`, use `defineOptions({ layout: AppLayout })`.
- If not using `<script setup>`, use `export default { layout: AppLayout }`.

## Sidebar Requirements
Treat the sidebar as workflow navigation, not decoration.

Navigation sections:

### Primary
- Dashboard
- Projects
- Production Queue
- Files
- Clients

### Management
- Users
- Activity Logs
- Reports

### System
- Settings

Implement all of the following:
- Active route highlighting
- Collapsible sidebar
- Collapsed-state persistence in `localStorage`
- Icon + label navigation entries

## Topbar Requirements
Topbar always includes:

Left side:
- Breadcrumb
- Page title

Right side:
- Quick create button
- Notifications bell
- User menu dropdown

User menu items:
- Profile
- Preferences
- Logout

## Workspace Rules
- Wrap all page content in `<PageContainer>`.
- Create `components/layout/PageContainer.vue`.
- Standard container classes: `max-w-7xl mx-auto p-6`.
- Do not let individual pages control outer spacing.

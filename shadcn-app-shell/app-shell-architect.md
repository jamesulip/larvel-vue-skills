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
- Require every page to render with `Head` + `AppLayout` wrapper.
- Canonical starter pattern:

```vue
<Head title="Dashboard" />
<AppLayout :breadcrumbs="breadcrumbs">
	<!-- page content -->
</AppLayout>
```

- `breadcrumbs` must be a page-local array of objects:
	- `{ title: string, href?: string }`
- Legacy `defineOptions({ layout: AppLayout })` may exist in older code, but this skill standardizes wrapper-based layout for new blank-app pages.

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

## Starter Default Pages
For blank app scaffolds, create these pages first:
- `Dashboard`
- `Users` (listing)
- `User Form` (form UI demo)
- `Settings`

Follow [blank-app-default-pages.md](blank-app-default-pages.md) for starter scope and structure.

## Skill-Creator Output Contract
- Every generated page must include `Head` title and wrapper-based `AppLayout` usage.
- Every generated page must pass `breadcrumbs` into `AppLayout`.
- All page body content must be placed inside `PageContainer`.
- Keep shell spacing, title hierarchy, and context consistent across generated pages.

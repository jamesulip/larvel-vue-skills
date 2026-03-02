# Skill 3 - app-data-table-standard

## Purpose
Standardize list pages around a default shadcn-vue table surface.

## Default Requirement
When asked to create a list page with a table, generate a page using plain shadcn-vue table primitives.

Use:
- `components/ui/table` (`Table`, `TableHeader`, `TableBody`, `TableRow`, `TableHead`, `TableCell`)

Do not default to `components/system/DataTable.vue`.

## Skill-Creator Triggers
Apply this skill when prompt intent includes any of:
- list page
- index page
- table page
- users list
- issues list

If prompt includes `minimal`, `simple`, or `ultra-minimal`, use the **Ultra-Minimal Starter Sample**.

## Skill-Creator Decision Rule
- If the prompt says "list", "index", or "table page" without asking for advanced table tooling, use plain shadcn-vue table primitives.
- Use `DataTable.vue` only when the prompt explicitly requests advanced table orchestration.

Mode selection:
- **Default mode**: use **Starter Sample Page**.
- **Minimal mode**: use **Ultra-Minimal Starter Sample**.
- **Advanced mode**: only when user explicitly asks for advanced table workflows.

## Default Output Contract
Generated default list pages should include:
- shadcn-vue table primitives for rendering rows/cells
- server-driven sorting and pagination hooks
- loading skeleton rows
- explicit empty state UI
- row-level actions via dropdown when actions are present
- shared page anatomy from [page-template-ui-consistency.md](page-template-ui-consistency.md)

Output schema for generated pages:
- `Head` title must match page context (`Users`, `Issues`, etc.)
- `AppLayout :breadcrumbs` must be present
- page body must be wrapped in `PageContainer`
- page header must follow shared title/description/actions placement
- table content must use `components/ui/table` primitives
- avoid custom design tokens and raw HTML table styling systems

## Starter Sample Page
Use this sample when generating a default list page.

Target: `resources/js/pages/Users/Index.vue`

```vue
<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue'
import EmptyState from '@/components/system/EmptyState.vue'
import {
	Table,
	TableBody,
	TableCell,
	TableHead,
	TableHeader,
	TableRow,
} from '@/components/ui/table'
import { Head } from '@inertiajs/vue3'

type UserRow = {
	id: number
	name: string
	email: string
	role: string
	status: 'active' | 'invited' | 'disabled'
}

const breadcrumbs = [
	{ title: 'Dashboard', href: '/dashboard' },
	{ title: 'Users', href: '/users' },
]

const users: UserRow[] = [
	{ id: 1, name: 'Ari Kim', email: 'ari@example.com', role: 'Admin', status: 'active' },
	{ id: 2, name: 'Noah Lee', email: 'noah@example.com', role: 'Editor', status: 'invited' },
]

const isLoading = false
</script>

<template>
	<Head title="Users" />

	<AppLayout :breadcrumbs="breadcrumbs">
		<div class="space-y-4">
			<div>
				<h1 class="text-xl font-semibold tracking-tight">Users</h1>
				<p class="text-muted-foreground text-sm">Manage workspace access and roles.</p>
			</div>

			<div v-if="isLoading" class="space-y-2">
				<div class="h-10 rounded-md border" />
				<div class="h-10 rounded-md border" />
				<div class="h-10 rounded-md border" />
			</div>

			<EmptyState
				v-else-if="users.length === 0"
				title="No users yet"
				description="Invite your first user to start collaborating."
			/>

			<Table v-else>
				<TableHeader>
					<TableRow>
						<TableHead>Name</TableHead>
						<TableHead>Email</TableHead>
						<TableHead>Role</TableHead>
						<TableHead>Status</TableHead>
					</TableRow>
				</TableHeader>
				<TableBody>
					<TableRow v-for="user in users" :key="user.id">
						<TableCell class="font-medium">{{ user.name }}</TableCell>
						<TableCell>{{ user.email }}</TableCell>
						<TableCell>{{ user.role }}</TableCell>
						<TableCell class="capitalize">{{ user.status }}</TableCell>
					</TableRow>
				</TableBody>
			</Table>
		</div>
	</AppLayout>
</template>
```

## Ultra-Minimal Starter Sample
Use this when the user asks for the simplest possible table page.

Target: `resources/js/pages/Issues/Index.vue`

```vue
<script setup lang="ts">
import { Head } from '@inertiajs/vue3'
import AppLayout from '@/layouts/AppLayout.vue'
import {
	Table,
	TableBody,
	TableCell,
	TableHead,
	TableHeader,
	TableRow,
} from '@/components/ui/table'

const breadcrumbs = [
	{ title: 'Dashboard', href: '/dashboard' },
	{ title: 'Issues', href: '/issues' },
]

const issues = [
	{ id: 'ENG-1023', title: 'Implement authentication flow', status: 'In Progress', updated: '2m ago' },
	{ id: 'ENG-1022', title: 'Update payment dependencies', status: 'Todo', updated: '1h ago' },
]
</script>

<template>
	<Head title="Issues" />

	<AppLayout :breadcrumbs="breadcrumbs">
		<div class="space-y-3">
			<h1 class="text-xl font-semibold tracking-tight">Issues</h1>

			<Table>
				<TableHeader>
					<TableRow>
						<TableHead>ID</TableHead>
						<TableHead>Title</TableHead>
						<TableHead>Status</TableHead>
						<TableHead class="text-right">Updated</TableHead>
					</TableRow>
				</TableHeader>

				<TableBody>
					<TableRow v-for="issue in issues" :key="issue.id">
						<TableCell class="font-mono text-xs">{{ issue.id }}</TableCell>
						<TableCell>{{ issue.title }}</TableCell>
						<TableCell>{{ issue.status }}</TableCell>
						<TableCell class="text-right text-muted-foreground">{{ issue.updated }}</TableCell>
					</TableRow>
				</TableBody>
			</Table>
		</div>
	</AppLayout>
</template>
```

## Optional Advanced Wrapper
`components/system/DataTable.vue` is optional and only for advanced modules that explicitly need extra table orchestration.

## Starter Minimum (Blank App)
For the default `Users` listing page in a blank app scaffold, require at minimum:
- Column sorting
- Server-side pagination
- Loading skeleton rows
- Explicit empty state

Starter-first rule:
- Do not block initial scaffold on full advanced table capabilities.
- Start with plain shadcn-vue table structure and clean spacing.
- Add advanced capabilities incrementally as needed.

## Skill-Creator Execution Steps
When generating a table page with this skill:
1. Select mode (Default / Minimal / Advanced) from prompt wording.
2. Apply the shared page template contract from [page-template-ui-consistency.md](page-template-ui-consistency.md).
3. Set page title and breadcrumbs.
4. Render table with shadcn-vue primitives.
5. Add loading and empty-state path unless prompt explicitly asks to omit.
6. Add optional row actions/pagination based on mode.

## Advanced Capabilities (Optional)
If the module explicitly requires a power-table workflow, add:
- Column sorting
- Server-side pagination
- Row selection
- Bulk actions
- Column visibility toggle
- Sticky header
- Loading skeleton rows

Keep the default list implementation plain shadcn-vue table unless advanced behavior is requested.

## Anti-Patterns
- Do not use custom token-heavy classes from external templates.
- Do not copy dense marketing/admin demo markup as-is.
- Do not introduce `DataTable.vue` unless requested.
- Do not omit `Head` and `AppLayout` wrapper contract.

## Row Behavior
- Row click opens the show/detail page.
- Checkbox click only selects the row.
- Actions column uses a dropdown menu.

## Visual Status Language
Use this fixed mapping:

| Status | Badge variant |
| --- | --- |
| pending | secondary |
| processing | warning |
| printing | warning |
| completed | success |
| on_hold | outline |
| cancelled | destructive |

Do not introduce freeform status colors.

## Acceptance Checklist
- Mode matches prompt intent (Default/Minimal/Advanced).
- Page uses `Head` and `AppLayout :breadcrumbs`.
- Page follows shared `PageContainer` + header template contract.
- Table uses shadcn-vue `Table*` primitives.
- Sample complexity matches request (especially for minimal prompts).
- No custom design-token styling copied from external templates.

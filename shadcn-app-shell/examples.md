# Examples: shadcn-app-shell

## Example 0: Deterministic Module Output Contract
When asked to generate a module named `Projects`, output this page set:
- `resources/js/pages/Projects/Index.vue`
- `resources/js/pages/Projects/Create.vue`
- `resources/js/pages/Projects/Edit.vue`
- `resources/js/pages/Projects/Show.vue`

All four pages must share:
- identical shell wrapper contract
- identical header/action placement
- identical spacing rhythm
- identical feedback behavior conventions

## Example 1: Resource Routes (`routes/web.php`)
```php
<?php

use App\Http\Controllers\ProjectController;
use Illuminate\Support\Facades\Route;

Route::middleware(['auth', 'verified'])->group(function () {
    Route::resource('projects', ProjectController::class);
    Route::delete('projects/bulk', [ProjectController::class, 'bulkDestroy'])->name('projects.bulk-destroy');
});
```

## Example 2: Controller (`app/Http/Controllers/ProjectController.php`)
```php
<?php

namespace App\Http\Controllers;

use App\Models\Project;
use Illuminate\Http\Request;
use Inertia\Inertia;
use Inertia\Response;

class ProjectController extends Controller
{
    public function index(Request $request): Response
    {
        $filters = $request->validate([
            'search' => ['nullable', 'string', 'max:120'],
            'status' => ['nullable', 'in:active,on_hold,completed'],
            'sort' => ['nullable', 'in:name,created_at'],
            'direction' => ['nullable', 'in:asc,desc'],
            'page' => ['nullable', 'integer', 'min:1'],
        ]);

        $query = Project::query();

        if (!empty($filters['search'])) {
            $query->where('name', 'like', '%' . $filters['search'] . '%');
        }

        if (!empty($filters['status'])) {
            $query->where('status', $filters['status']);
        }

        $sort = $filters['sort'] ?? 'created_at';
        $direction = $filters['direction'] ?? 'desc';

        $projects = $query
            ->orderBy($sort, $direction)
            ->paginate(15)
            ->withQueryString();

        return Inertia::render('Projects/Index', [
            'projects' => $projects,
            'filters' => [
                'search' => $filters['search'] ?? '',
                'status' => $filters['status'] ?? '',
                'sort' => $sort,
                'direction' => $direction,
            ],
        ]);
    }

    public function create(): Response
    {
        return Inertia::render('Projects/Create');
    }

    public function store(Request $request)
    {
        $validated = $request->validate([
            'name' => ['required', 'string', 'max:120'],
            'status' => ['required', 'in:active,on_hold,completed'],
            'description' => ['nullable', 'string', 'max:1000'],
        ]);

        $project = Project::create($validated);

        return redirect()
            ->route('projects.edit', $project)
            ->with('success', 'Project created.');
    }

    public function show(Project $project): Response
    {
        return Inertia::render('Projects/Show', [
            'project' => $project,
        ]);
    }

    public function edit(Project $project): Response
    {
        return Inertia::render('Projects/Edit', [
            'project' => $project,
        ]);
    }

    public function update(Request $request, Project $project)
    {
        $validated = $request->validate([
            'name' => ['required', 'string', 'max:120'],
            'status' => ['required', 'in:active,on_hold,completed'],
            'description' => ['nullable', 'string', 'max:1000'],
        ]);

        $project->update($validated);

        return redirect()
            ->route('projects.edit', $project)
            ->with('success', 'Project updated.');
    }

    public function destroy(Project $project)
    {
        $project->delete();

        return redirect()
            ->route('projects.index')
            ->with('success', 'Project deleted.');
    }
}
```

## Example 3: List Page (`resources/js/pages/Projects/Index.vue`)
```vue
<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue'
import PageContainer from '@/components/layout/PageContainer.vue'
import EmptyState from '@/components/system/EmptyState.vue'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import {
  Table,
  TableBody,
  TableCell,
  TableHead,
  TableHeader,
  TableRow,
} from '@/components/ui/table'
import { Head, Link, router } from '@inertiajs/vue3'
import { reactive } from 'vue'

type ProjectRow = {
  id: number
  name: string
  status: 'active' | 'on_hold' | 'completed'
  created_at: string
}

const props = defineProps<{
  projects: {
    data: ProjectRow[]
    links: Array<{ url: string | null; label: string; active: boolean }>
  }
  filters: {
    search: string
    status: string
    sort: string
    direction: string
  }
}>()

const breadcrumbs = [
  { title: 'Dashboard', href: '/dashboard' },
  { title: 'Projects', href: '/projects' },
]

const filters = reactive({
  search: props.filters.search ?? '',
  status: props.filters.status ?? '',
})

const submitFilters = () => {
  router.get('/projects', filters, {
    preserveState: true,
    replace: true,
  })
}

const resetFilters = () => {
  filters.search = ''
  filters.status = ''
  submitFilters()
}
</script>

<template>
  <Head title="Projects" />

  <AppLayout :breadcrumbs="breadcrumbs">
    <PageContainer>
      <section class="space-y-4">
        <header class="flex flex-col gap-3 sm:flex-row sm:items-start sm:justify-between">
          <div class="space-y-1">
            <h1 class="text-xl font-semibold tracking-tight">Projects</h1>
            <p class="text-sm text-muted-foreground">Track delivery progress and ownership.</p>
          </div>
          <div class="flex items-center gap-2">
            <Button as-child>
              <Link href="/projects/create">Create Project</Link>
            </Button>
          </div>
        </header>

        <div class="flex flex-col gap-2 sm:flex-row">
          <Input
            v-model="filters.search"
            placeholder="Search projects"
            class="sm:max-w-xs"
            @keyup.enter="submitFilters"
          />
          <div class="flex items-center gap-2">
            <Button variant="secondary" @click="submitFilters">Apply</Button>
            <Button variant="ghost" @click="resetFilters">Reset</Button>
          </div>
        </div>

        <EmptyState
          v-if="projects.data.length === 0"
          title="No projects yet"
          description="Create the first project to start tracking work."
        />

        <Table v-else>
          <TableHeader>
            <TableRow>
              <TableHead>Name</TableHead>
              <TableHead>Status</TableHead>
              <TableHead class="text-right">Actions</TableHead>
            </TableRow>
          </TableHeader>
          <TableBody>
            <TableRow v-for="project in projects.data" :key="project.id">
              <TableCell class="font-medium">{{ project.name }}</TableCell>
              <TableCell class="capitalize">{{ project.status }}</TableCell>
              <TableCell class="text-right">
                <div class="inline-flex items-center gap-2">
                  <Link class="text-sm underline" :href="`/projects/${project.id}`">View</Link>
                  <Link class="text-sm underline" :href="`/projects/${project.id}/edit`">Edit</Link>
                </div>
              </TableCell>
            </TableRow>
          </TableBody>
        </Table>
      </section>
    </PageContainer>
  </AppLayout>
</template>
```

## Example 4: Form Page (`resources/js/pages/Projects/Edit.vue`)
```vue
<script setup lang="ts">
import AppLayout from '@/layouts/AppLayout.vue'
import PageContainer from '@/components/layout/PageContainer.vue'
import FormSection from '@/components/form/FormSection.vue'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { Label } from '@/components/ui/label'
import { Head, Link, router, useForm } from '@inertiajs/vue3'

const props = defineProps<{
  project: {
    id: number
    name: string
    status: 'active' | 'on_hold' | 'completed'
    description: string | null
  }
}>()

const breadcrumbs = [
  { title: 'Dashboard', href: '/dashboard' },
  { title: 'Projects', href: '/projects' },
  { title: 'Edit', href: `/projects/${props.project.id}/edit` },
]

const form = useForm({
  name: props.project.name,
  status: props.project.status,
  description: props.project.description ?? '',
})

const save = () => form.put(`/projects/${props.project.id}`)
const saveAndClose = () =>
  form.put(`/projects/${props.project.id}`, {
    onSuccess: () => router.visit('/projects'),
  })
</script>

<template>
  <Head :title="`Edit ${project.name}`" />

  <AppLayout :breadcrumbs="breadcrumbs">
    <PageContainer>
      <section class="space-y-6">
        <header class="flex flex-col gap-3 sm:flex-row sm:items-start sm:justify-between">
          <div class="space-y-1">
            <h1 class="text-xl font-semibold tracking-tight">Edit Project</h1>
            <p class="text-sm text-muted-foreground">Update project metadata and status.</p>
          </div>
        </header>

        <FormSection title="General Information">
          <div class="grid gap-4 sm:grid-cols-2">
            <div class="space-y-2">
              <Label for="name">Name</Label>
              <Input id="name" v-model="form.name" />
              <p v-if="form.errors.name" class="text-sm text-destructive">{{ form.errors.name }}</p>
            </div>
            <div class="space-y-2">
              <Label for="status">Status</Label>
              <Input id="status" v-model="form.status" />
              <p v-if="form.errors.status" class="text-sm text-destructive">{{ form.errors.status }}</p>
            </div>
          </div>
        </FormSection>

        <div class="flex justify-end gap-2">
          <Button variant="ghost" as-child>
            <Link href="/projects">Cancel</Link>
          </Button>
          <Button variant="secondary" :disabled="form.processing" @click="saveAndClose">
            Save &amp; Close
          </Button>
          <Button :disabled="form.processing" @click="save">
            {{ form.processing ? 'Saving...' : 'Save' }}
          </Button>
        </div>
      </section>
    </PageContainer>
  </AppLayout>
</template>
```

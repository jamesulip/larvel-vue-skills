# Rules: shadcn-app-shell

## 1) Application-Shell Ownership (Non-Negotiable)
- Every authenticated page must belong to a resource.
- Every page must map to a Laravel route.
- Every page must receive props from a Laravel controller via `Inertia::render`.
- Never generate standalone Vue pages that fetch core page data with `axios`/`fetch`.
- Never bypass the shared shell for authenticated pages.

## 2) Page Layout Contract (Non-Negotiable)
Every page must follow:

```vue
<Head title="..." />
<AppLayout :breadcrumbs="breadcrumbs">
  <PageContainer>
    <section class="space-y-4">
      <header class="flex flex-col gap-3 sm:flex-row sm:items-start sm:justify-between">
        <div class="space-y-1">
          <h1 class="text-xl font-semibold tracking-tight">...</h1>
          <p class="text-sm text-muted-foreground">...</p>
        </div>
        <div class="flex items-center gap-2"><!-- actions --></div>
      </header>
      <!-- page content -->
    </section>
  </PageContainer>
</AppLayout>
```

Constraints:
- No full-width freeform page shells.
- No per-page custom outer spacing wrappers.
- Use one `h1` per page.

## 3) Page Header Rules
Page header must contain:
- Title (resource name)
- Description (operational context)
- Primary action slot (top-right on desktop)

Constraints:
- Primary action must not be hidden in table rows or deep inside cards.
- Header action placement must remain consistent across modules.

## 4) Spacing and Structure Rules
- Maintain vertical rhythm:
  - header -> content
  - filters -> table
  - form section -> next section
- Use `space-y-4` baseline; `space-y-6` allowed for form-heavy pages.
- Avoid dense stacking with no breathing room.
- Avoid large unused gaps.

## 5) Card Usage Rules
Cards are functional containers only.

Allowed:
- tables
- forms
- detail panels
- metrics blocks

Disallowed:
- wrapping the entire page just for decoration
- deep nested cards without functional separation

## 6) Table/List Rules
Default order for resource index pages:
1. Header
2. Filter bar
3. Table
4. Pagination

Required for every list page:
- search
- pagination
- explicit empty state
- loading state (skeleton rows or equivalent)

Action rules:
- row actions are right-aligned
- destructive actions are dangerous style in row menu or confirmation flow
- bulk actions only render when selection exists

## 7) Filter Rules
- Filters live above the table in a dedicated bar.
- Filters must be resettable.
- Avoid unpredictable multi-line wrapping that pushes content excessively.
- Do not hide primary filters in modals.
- Use query-string-based filters with server-driven results.

## 8) Form Rules
Field structure must be consistent:
1. section title
2. field label
3. input/control
4. validation message
5. optional help text

Validation rules:
- render backend validation from `form.errors`
- validation messages appear directly below field
- never use browser `alert()` or modal alerts for field validation

Submission rules:
- use `useForm` for mutation requests
- disable submit while processing
- show loading state on submit button
- prevent double submit

Action placement:
- submit actions are bottom-right
- primary: `Save`
- secondary: `Save & Close`
- tertiary: `Cancel`

## 9) Detail/Show Rules
Structure:
1. Header
2. Primary information card
3. Secondary sections

Constraints:
- show page must be read-oriented
- do not reuse edit form as show page

## 10) Inertia and CRUD Contract
- Read pages: GET route + controller query + `Inertia::render`.
- Mutations: `useForm` -> POST/PUT/PATCH/DELETE.
- After successful mutation:
  - redirect to deterministic target (index, show, or edit)
  - include feedback (`success` flash/toast path)

Required resource naming:
- index
- create
- store
- show
- edit
- update
- destroy

## 11) Anti-Patterns
- Marketing-site layouts for internal modules
- Decorative animation-heavy interfaces
- Random per-module spacing and header styles
- Different action placement per resource
- Copying external admin template token systems into one module only
- Fake frontend-only data contracts disconnected from Laravel controllers

## 12) Completion Checks
A generated page is valid only if all are true:
- Uses `Head + AppLayout + PageContainer`
- Uses shared header anatomy (title/description/actions)
- Preserves consistent spacing rhythm
- Uses server-owned props from controller
- Has explicit loading/empty/error feedback paths where relevant
- Keeps actions in expected locations (header/row/form footer)

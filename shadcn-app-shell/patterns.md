# Patterns: shadcn-app-shell

## Pattern 1: New Resource Module Generation
Use when prompt asks for a new module (example: Projects, Clients, Orders).

Steps:
1. Define resource slug and route base (`projects`).
2. Create/confirm RESTful routes.
3. Create/confirm controller actions for CRUD.
4. Build page set:
   - `Resource/Index.vue`
   - `Resource/Create.vue`
   - `Resource/Edit.vue`
   - `Resource/Show.vue`
5. Apply shell layout contract to every page.
6. Add consistent navigation entry in same menu group as related resources.
7. Validate list/form/show behavior using checks below.

Validation gates:
- every page has breadcrumbs and shared header anatomy
- every page receives controller props
- mutation pages use `useForm`

## Pattern 2: List Page Blueprint (`Index`)
Layout sequence:
1. Page Header
2. Filter Bar
3. Table Container
4. Pagination Row

Implementation flow:
1. Parse query inputs in controller (`search`, `status`, `sort`, `direction`, `page`).
2. Build query with conditional filters/sort.
3. Paginate and append query string.
4. Return list + filter snapshot in `Inertia::render`.
5. In Vue page:
   - initialize local filter model from props
   - submit filters via Inertia GET with `replace` + `preserveState`
   - render loading/empty/ready states
6. Add row action menu (`show`, `edit`, `delete`).
7. Add bulk toolbar only when row selections exist.

Edge handling:
- zero records -> empty state in table area with create action
- deleted current-page last record -> redirect/refresh to valid page

## Pattern 3: Create/Edit Form Blueprint
Shared layout:
1. Header
2. Form sections (`FormSection`)
3. Sticky or footer action row (Save / Save & Close / Cancel)

Implementation flow:
1. Define `useForm` model from server props/defaults.
2. Build sectioned fields with labels and message slots.
3. On submit:
   - `form.post(...)` for create
   - `form.put(...)` or `form.patch(...)` for edit
4. On validation failure:
   - show field error below field
   - focus first invalid control
5. On success:
   - `Save`: stay on page and refresh data/feedback
   - `Save & Close`: redirect to index
6. Cancel behavior:
   - if dirty: confirm intent
   - if clean: navigate back immediately

Edge handling:
- prevent duplicate submit during `form.processing`
- preserve user input on validation errors

## Pattern 4: Show Page Blueprint
Layout sequence:
1. Header with edit action
2. Primary summary/info card
3. Secondary cards (activity, metadata, related records)

Rules:
- no editable controls by default on show page
- include fast path to edit
- related tables follow same list conventions when present

## Pattern 5: Filter Bar Blueprint
Use controls aligned to resource needs:
- text search
- status/select filters
- date range when operationally required

Flow:
1. Keep filter state in page model.
2. Trigger Inertia GET on submit/debounce.
3. Preserve scroll/state where needed.
4. Include `Reset` action restoring canonical defaults.

## Pattern 6: Action Placement Blueprint
- `Create/Add/Upload`: page header right
- `Export`: header secondary action
- `Edit`: row action or show-header action
- `Delete`: row action with confirmation
- `Bulk Delete`: bulk toolbar only when selected > 0

Do not move these placements per module.

## Pattern 7: Feedback and Error Blueprint
- Validation errors: inline field messages
- Server operation failure: toast error + keep context
- Success: toast success + deterministic redirect target
- Loading:
  - list pages: skeleton rows
  - forms: button loading + disabled submit

Never block entire page with fullscreen spinner for standard CRUD operations.

## Pattern 8: Deterministic Refactor of Inconsistent Page
Use when existing page violates shell consistency.

Steps:
1. Wrap with `Head + AppLayout + PageContainer`.
2. Replace custom page top section with shared header anatomy.
3. Normalize action placement to contract.
4. Normalize spacing rhythm.
5. Convert ad-hoc table/form markup to shadcn-vue primitives.
6. Verify no regression in route/controller/props contract.

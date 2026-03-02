# Skill: shadcn-app-shell

## Capability
Enforce a deterministic Laravel + Inertia + Vue application-shell UI contract for internal dashboard pages using shadcn-vue primitives.

## Primary Outcome
Generated pages must look and behave like one product:
- same shell
- same page anatomy
- same spacing rhythm
- same action placement
- same CRUD behavior

## Use This Skill When
- Generating any authenticated page or page template
- Building CRUD modules (`index`, `create`, `store`, `show`, `edit`, `update`, `destroy`)
- Building tables, filters, pagination, row actions, bulk actions
- Building create/edit forms with server validation
- Refactoring inconsistent pages to app-shell conventions

## Do Not Use This Skill For
- Marketing pages
- Landing pages
- Public brochure layouts
- Standalone SPA-only experiments without Laravel route/controller ownership

## Deterministic Activation
If prompt includes any of these intents, activate this skill:
- "create page", "template page", "module", "crud", "form", "list", "index", "show page"
- "make UI consistent", "same layout", "same UX", "dashboard style"

## Decision Protocol
1. Identify resource name and route scope.
2. Determine page type:
   - List: `index`
   - Create: `create`
   - Edit: `edit`
   - Detail: `show`
3. Enforce backend ownership:
   - page must map to Laravel route
   - route must map to controller action
   - controller must return `Inertia::render(...)` with props
4. Enforce shell contract from `rules.md` before writing page markup.
5. Apply page-specific blueprint from `patterns.md`.
6. Validate completion using `rules.md` acceptance checks.

## Generation Preference
- Prefer conformity over creativity.
- Prefer predictable operator workflows over unique page designs.
- Prefer reusable primitives over one-off custom layout systems.

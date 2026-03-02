# Page Template UI Consistency Standard

## Purpose
Ensure every generated internal page/template uses the same UI/UX language so operators do not relearn layout patterns between modules.

## Required Baseline Contract
Every generated page in authenticated scope must follow this shape:

```vue
<Head title="Page Title" />
<AppLayout :breadcrumbs="breadcrumbs">
  <PageContainer>
    <section class="space-y-4">
      <header class="flex flex-col gap-3 sm:flex-row sm:items-start sm:justify-between">
        <div class="space-y-1">
          <h1 class="text-xl font-semibold tracking-tight">Page Title</h1>
          <p class="text-muted-foreground text-sm">Short operational context.</p>
        </div>
        <div class="flex items-center gap-2">
          <!-- page actions -->
        </div>
      </header>

      <!-- page body -->
    </section>
  </PageContainer>
</AppLayout>
```

Use this contract for dashboard, index, create/edit, and settings pages unless the user explicitly asks for a different layout.

## Consistency Rules
- Use one page shell pattern across modules: `Head` + `AppLayout :breadcrumbs` + `PageContainer` + header block + content block.
- Keep `breadcrumbs` page-local and pass objects as `{ title: string, href?: string }`.
- Keep page title/description hierarchy consistent:
  - Title: `text-xl font-semibold tracking-tight`
  - Description: `text-sm text-muted-foreground`
- Keep spacing rhythm predictable:
  - Page-level sections: `space-y-4`
  - Form-heavy pages may use `space-y-6`
  - Do not introduce random per-page outer margin/padding wrappers
- Use the same action placement rule: primary actions stay in top-right header action group on desktop and stack naturally on mobile.

## Component Surface Rules
- Use shadcn-vue primitives as the default surface language.
- Lists/index pages: use `components/ui/table` primitives by default.
- Forms: use sectioned blocks via `FormSection`.
- Empty and sparse states: use shared `EmptyState` component patterns.
- Avoid mixing multiple visual systems in one page (custom token sets, copied external admin templates, and bespoke spacing systems).

## State and Feedback Rules
- Every data-rendering page must provide explicit loading, empty, and ready states.
- Every mutating form must provide pending submit state and validation error rendering.
- Use consistent feedback channels:
  - toast for global success/error feedback
  - inline field/section errors for form validation

## Accessibility and Usability Rules
- Use one semantic page heading (`h1`) per page.
- Preserve readable action labels (`Save`, `Save & Close`, `Cancel`) and avoid ambiguous CTA text.
- Keep target sizes and spacing comfortable for dense operational use.
- Preserve keyboard-operable controls for tables, forms, and menus.

## Anti-Patterns
- Do not generate a different page chrome for each module.
- Do not skip `PageContainer` and handcraft unique outer spacing on each page.
- Do not switch heading, action placement, or spacing patterns without explicit user request.
- Do not apply decorative styles that reduce scan speed.

## Output Acceptance Checklist
- Page uses `Head` + `AppLayout :breadcrumbs` + `PageContainer`.
- Header block order is: title/description left, actions right.
- Title and description typography match the shared hierarchy.
- Page includes explicit loading/empty/ready handling when data is shown.
- Page uses shared shadcn-vue primitives, not ad-hoc template styling.
- Navigation context and spacing are consistent with other generated pages.

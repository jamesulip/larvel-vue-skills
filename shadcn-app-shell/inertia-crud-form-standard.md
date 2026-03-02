# Skill 4 - inertia-crud-form-standard

## Purpose
Treat forms as workspace panels, not standalone simple pages.

## Starter Minimum (Blank App)
For the default `User Form` starter page, require:
- Sectioned card layout using `FormSection`
- Validation rendering from `form.errors`
- Submit loading state
- Dirty-state confirmation on cancel

Starter-first rule:
- Keep the first scaffold minimal but complete.
- Add advanced section depth and workflow-specific controls after baseline behavior is in place.

## Skill-Creator Default Contract
When asked for "form page", "create page", or "edit page" in starter scope:
- apply shared page template anatomy from [page-template-ui-consistency.md](page-template-ui-consistency.md)
- generate sectioned form UI using `FormSection`
- render backend errors from `form.errors`
- show pending submit state on primary action
- include cancel behavior with dirty-state confirmation

## Form Structure
Implement card-based forms with sectioned content, for example:

```text
ProjectForm
├─ General Information
├─ Production Settings
├─ Assignment
└─ Notes
```

Wrap each section as:
- `<FormSection title="General Information">`

Create:
- `components/form/FormSection.vue`
- `FormSection` is a local Vue UI component used inside Inertia pages, not an Inertia-provided component.

## Validation Integration
Use Laravel validation as the only source of truth.

Implement all of the following:
- Render backend validation errors from `form.errors`.
- Auto-focus the first invalid input after failed submit.
- Scroll to the first error section or field.
- Show loading spinner on submit button while request is pending.
- Prevent double submit while pending.

## Save UX
Support these actions:

| Button | Behavior |
| --- | --- |
| Save | Stay on page |
| Save & Close | Redirect to index |
| Cancel | Confirm if form is dirty |

Dirty detection is mandatory.

## Consistency Addendum
- Keep form pages inside shared wrapper anatomy: `Head` + `AppLayout :breadcrumbs` + `PageContainer`.
- Keep page header placement consistent with list/settings pages (title/description left, actions right).
- Keep primary/secondary action ordering consistent across forms:
  - Primary: `Save`
  - Secondary: `Save & Close`
  - Tertiary: `Cancel`

# Skill 4 - inertia-crud-form-standard

## Purpose
Treat forms as workspace panels, not standalone simple pages.

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

# Skill 5 - system-feedback-standard

## Purpose
Provide clear, immediate operational feedback for every system action.

## Starter Minimum (Blank App)
Default starter pages (`Dashboard`, `Users`, `User Form`, `Settings`) must include:
- Page-load skeletons where data is fetched
- Submit button spinner for form submissions
- Success/failure toast for create/update actions
- Explicit empty state for list-like surfaces

Do not delay starter scaffolding for advanced progress workflows.

## Skill-Creator Default Contract
For starter output, always include at least:
- one loading state pattern where data loads
- one success/failure toast path for mutations
- one explicit empty state path for list surfaces

## Toast Notifications
Use toast notifications for:
- Saved
- Updated
- Deleted
- Queued

Do not use `alert()`.

## Loading Feedback
Use this behavior by operation type:

| Operation | UI feedback |
| --- | --- |
| Page load | Skeleton |
| Form submit | Button spinner |
| Background action | Toast: `Processing...` |
| Long process | Progress indicator |

## Empty States
Create and use:
- `components/system/EmptyState.vue`

Every module must render an explicit empty state instead of blank space.

Example:
- Title: `No projects yet`
- Description: `Create your first {EntitySingular} to begin tracking work.`
- Action: `Create Project`

Tables must never render blank whitespace when data is empty.

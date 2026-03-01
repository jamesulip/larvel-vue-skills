# Skill 5 - system-feedback-standard

## Purpose
Provide clear, immediate operational feedback for every system action.

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

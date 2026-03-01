# Skill 3 - app-data-table-standard

## Purpose
Standardize list pages around a high-productivity table surface.

## Required Component
- `components/system/DataTable.vue`

All business modules must use this component for list/index screens.

## Mandatory Capabilities
Implement all of the following:
- Column sorting
- Server-side pagination
- Row selection
- Bulk actions
- Column visibility toggle
- Sticky header
- Loading skeleton rows

Do not use plain `<table>` implementations for business modules.

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

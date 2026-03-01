# Skill 2 - workspace-navigation

## Purpose
Make navigation feel like a desktop application, not a series of disconnected web pages.

## Breadcrumb System
- Generate breadcrumbs from route names and route metadata.
- Require route metadata for breadcrumb labels, for example: `meta: { breadcrumb: "Projects" }`.
- Support deep trails such as: `Projects / {EntityLabel} #{id} / Production`.

## Remembered Page State
On filter changes, pagination changes, sorting changes, and table navigation:
- Use `preserveState: true`.
- Use `preserveScroll: true`.

## Keyboard UX
Implement these shortcuts globally for internal productivity:

- `Ctrl + K`: open global search
- `N`: create new record
- `/`: focus search field
- `Esc`: close dialogs and overlays

Create:
- `components/system/CommandPalette.vue`

## Behavior Notes
- Scope shortcuts to avoid conflicts while typing in input fields.
- Keep command execution deterministic and fast.

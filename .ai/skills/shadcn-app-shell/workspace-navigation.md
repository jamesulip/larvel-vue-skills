# Skill 2 - workspace-navigation

## Purpose
Make navigation feel like a desktop application, not a series of disconnected web pages.

## Breadcrumb System
- Define breadcrumbs per page and pass them into `AppLayout`.
- Use page-local `breadcrumbs` arrays with objects: `{ title: string, href?: string }`.
- Support deep trails such as: `Projects / {EntityLabel} #{id} / Production`.
- Do not depend on Vue Router metadata for breadcrumb generation in Inertia pages.

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

## Skill-Creator Guidance
- Default breadcrumbs must be page-local and passed through `AppLayout`.
- For starter pages, prioritize preserved state/scroll on table filter and pagination interactions.
- Keyboard shortcuts are optional in starter output unless explicitly requested.

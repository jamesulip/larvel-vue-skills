# Skill 6 - production-workflow-awareness

## Purpose
Model records as work units in a production pipeline, not as content entries.

## Lifecycle Model
Represent the lifecycle as:

`created -> queued -> processing -> completed`

With alternate exits from in-flight work:
- `on_hold`
- `cancelled`

## UI Requirements
The UI must:
- Visually show progress stage for each work unit.
- Highlight active work units.
- Emphasize actionable items and bottlenecks.

## Dashboard Requirements
Dashboard views must expose dynamic lifecycle metrics for the current entity type, including:
- Active `{EntityPlural}`
- Overdue `{EntityPlural}`
- `{EntityPlural}` waiting approval
- Today's completions

## Operational Priority
Bias list ordering and emphasis toward work units that need operator action now.

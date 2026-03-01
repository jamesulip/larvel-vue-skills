# Page Props Typing

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | high | Type page props explicitly for reliable component contracts | typescript, props, usePage, defineProps |

Type all page props and shared props when TypeScript is enabled.

## Agent Directives

- Trigger: TypeScript-enabled pages/composables.
- Must: declare explicit prop/page interfaces.
- Must Not: default to `any` for page props.
- Auto: type `usePage<T>()` and `defineProps<T>()` consistently.

## Bad Example

```ts
const page = usePage<any>()
```

## Good Example

```ts
interface PageProps {
  users: Array<{ id: number; name: string }>
}

const page = usePage<PageProps>()
```

## Why

- Prevents runtime shape mismatches.
- Improves IDE support and refactor safety.

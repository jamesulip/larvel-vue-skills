# External Link Handling

| section | priority | description | keywords |
| --- | --- | --- | --- |
| pages-layouts | medium | Use normal anchors for external URLs; reserve Inertia Link for internal routes | external, anchor, target, rel |

Use `<a>` for external destinations and `Link` for internal app navigation.

## Agent Directives

- Trigger: rendering links to non-app domains.
- Must: use `<a>` with `target`/`rel` for external URLs.
- Must Not: use Inertia `Link` for external destinations.
- Auto: enforce `rel="noopener noreferrer"` with `target="_blank"`.

## Bad Example

```vue
<Link href="https://docs.example.com">Docs</Link>
```

## Good Example

```vue
<a href="https://docs.example.com" target="_blank" rel="noopener noreferrer">Docs</a>
```

## Why

- Keeps protocol semantics clear.
- Avoids unintended Inertia interception on external URLs.

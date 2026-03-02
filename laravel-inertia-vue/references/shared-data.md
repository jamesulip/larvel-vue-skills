# Shared Data and Context

## Shared Props
Use `HandleInertiaRequests` to share cross-page context:
- Auth user summary
- Permissions/capabilities
- Flash messages
- Workspace metadata (active tenant/team/site)

Keep shared payloads small and stable.

## Access in Vue Pages
Use `usePage()` to read shared props and type them in page code.

```ts
const page = usePage<{
  auth: { user: { id: number; name: string } | null };
  flash: { success?: string; error?: string };
}>();
```

## Flash + Feedback Pattern
- Set flash messages in Laravel after mutations.
- Show them via toast system on next Inertia response.
- Avoid one-off alert dialogs for success/failure notifications.

## Authorization Visibility
- Prefer passing `can` maps from server for action visibility.
- Do not rely on client-only role checks for protected actions.

# Navigation and State

## Link and Visit Conventions
- Use `<Link>` for declarative navigation.
- Use `router.get/post/put/patch/delete` for action-driven navigation.
- Prefer named route helpers and params over hardcoded URLs.

## Preserve UX Context
For filters, sorting, and pagination changes:

- `preserveState: true`
- `preserveScroll: true`
- `replace: true` when updating query params in-place

Example:

```ts
router.get(route("projects.index"), nextFilters, {
  preserveState: true,
  preserveScroll: true,
  replace: true,
  only: ["projects", "filters"],
});
```

## Remember Local UI State
Use `useRemember` for local state that must survive navigation:

```ts
const filters = useRemember({ search: "", status: "all" }, "projects.filters");
```

## Partial Reloads
- Use `only` to reload required props.
- Use `except` when excluding expensive props.
- Avoid full page reloads for routine data-table interactions.

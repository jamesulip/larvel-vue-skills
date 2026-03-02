# Page and Layout Patterns

## Directory Conventions
- Put pages under `resources/js/pages`.
- Put persistent layouts under `resources/js/layouts`.
- Put shared UI components under `resources/js/components`.

## Page Component Baseline
Use `<script setup lang="ts">` for Inertia pages:

```vue
<script setup lang="ts">
import AppLayout from "@/layouts/AppLayout.vue";

defineOptions({ layout: AppLayout });

interface Props {
  title: string;
}

defineProps<Props>();
</script>
```

## Layout Persistence Rule
- Assign the layout at page-level (`defineOptions({ layout: AppLayout })`).
- Keep shell structure in the layout component and render page content via slot.
- Do not duplicate shell wrappers in each page.

## Controller-to-Page Contract
- Keep page names stable (`Inertia::render('Module/Index')` maps to `pages/Module/Index.vue`).
- Keep prop keys explicit and predictable (`items`, `filters`, `meta`, `can`).
- Use API resources or transformers when prop shape is reused across pages.

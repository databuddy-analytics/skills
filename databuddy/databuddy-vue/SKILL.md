# Vue SDK (`@databuddy/sdk/vue`)

Vue 3 integration: tracker component, flags plugin, and composables.

## Exports

- `Databuddy` — Vue component that injects the tracker script
- `createFlagsPlugin(options)` — Vue plugin factory for feature flags
- `useFlags()` — Composable for full flags context
- `useFlag(key)` — Composable for a single flag

## `<Databuddy />` Component

Injects the tracker script on mount, removes on unmount. Watches props and re-injects on change. Renders nothing.

```vue
<script setup>
import { Databuddy } from "@databuddy/sdk/vue";
</script>

<template>
  <Databuddy track-web-vitals track-errors />
</template>
```

Accepts all `DatabuddyConfig` props (kebab-case in templates). Auto-detects `clientId` from environment.

### In App Root

```typescript
// main.ts
import { createApp } from "vue";
import App from "./App.vue";

createApp(App).mount("#app");
```

```vue
<!-- App.vue -->
<script setup>
import { Databuddy } from "@databuddy/sdk/vue";
</script>

<template>
  <RouterView />
  <Databuddy track-web-vitals track-errors :disabled="isDev" />
</template>
```

## Feature Flags

### Plugin Setup

```typescript
import { createApp } from "vue";
import { createFlagsPlugin } from "@databuddy/sdk/vue";

const app = createApp(App);
app.use(createFlagsPlugin({
  clientId: "your-client-id",
  user: { userId: "user-123" },
  environment: "production",
}));
app.mount("#app");
```

### useFlag(key)

Returns reactive computed refs:

```vue
<script setup>
import { useFlag } from "@databuddy/sdk/vue";

const { on, loading, state } = useFlag("new-feature");
</script>

<template>
  <div v-if="loading">Loading...</div>
  <NewFeature v-else-if="on" />
  <OldFeature v-else />
</template>
```

Return type:
- `on: ComputedRef<boolean>` — Whether the flag is enabled
- `loading: ComputedRef<boolean>` — Whether the flag is still loading
- `state: ComputedRef<FlagState>` — Full flag state including `value`, `variant`, `status`

### useFlags()

Returns the full flags API. Throws if the plugin is not installed.

```typescript
const { getFlag, fetchAllFlags, updateUser, refresh, updateConfig, memoryFlags } = useFlags();

// Imperative flag check
const state = getFlag("my-feature"); // FlagState

// Update user after login
updateUser({ userId: "user-123", email: "user@example.com" });

// Force refresh all flags
await refresh(true); // forceClear = true

// Access all cached flags
console.log(memoryFlags); // Record<string, FlagResult>
```

See [flags skill](../databuddy-flags/SKILL.md) for full types and caching details.

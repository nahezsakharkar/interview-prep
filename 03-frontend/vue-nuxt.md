---
title: "Vue and Nuxt.js"
tags: ["frontend","vue","nuxt"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Vue and Nuxt.js

## Definition

Vue.js is a progressive JavaScript framework for building user interfaces. Nuxt.js is a high-level framework built on top of Vue that provides server-side rendering (SSR), static site generation (SSG), and an intuitive file-system-based routing system.

## Vue.js Core Concepts

### 1. Reactivity System
Vue uses a proxy-based reactivity system (in Vue 3). When a reactive property is accessed, it is "tracked"; when it is modified, it "triggers" the update of all dependent components.

### 2. Composition API vs Options API
- **Options API**: Organizes code by property (e.g., `data`, `methods`, `computed`). Great for small components but becomes messy in large ones.
- **Composition API**: Uses the `setup()` function (or `<script setup>`) to organize code by *logical concern*. This allows for better logic reuse via "Composables" (similar to React Hooks).

### 3. Virtual DOM
Like React, Vue uses a Virtual DOM to minimize actual DOM manipulations. However, Vue's compiler optimizes the process by marking "static" content, allowing the diffing algorithm to skip parts of the tree that never change.

## Nuxt.js Core Concepts

### 1. Rendering Modes
- **SSR (Server-Side Rendering)**: Renders the page on the server for every request. Ideal for dynamic content and SEO.
- **SSG (Static Site Generation)**: Renders pages at build time. Extremely fast and can be hosted on a CDN.
- **ISR (Incremental Static Regeneration)**: Regenerates static pages in the background after a certain interval.

### 2. File-System Routing
In Nuxt, any `.vue` file created in the `pages/` directory automatically becomes a route. For example, `pages/about.vue` maps to `/about`.

### 3. Auto-Imports
Nuxt automatically imports components in the `components/` directory and composables in the `composables/` directory, reducing boilerplate.

## Comparison: Vue vs. React

| Feature | Vue.js | React |
| :--- | :--- | :--- |
| **Learning Curve** | Gentler (Template-based) | Steeper (JSX/JS-heavy) |
| **State Management** | Pinia (Official) | Redux / Zustand / Context |
| **Reactivity** | Automatic (Proxies) | Manual (`useState` / `useEffect`) |
| **Templates** | HTML-based templates | JSX |

## Working Code Example

This example demonstrates a Vue 3 component using the **Composition API** and a Nuxt-style data fetching pattern.

```vue
<script setup>
import { ref, computed, onMounted } from 'vue';

// State (Reactive)
const count = ref(0);
const items = ref([]);

// Computed property (automatically updates when count changes)
const doubleCount = computed(() => count.value * 2);

// Method
const increment = () => {
  count.value++;
};

// Nuxt-style async data fetching
onMounted(async () => {
  try {
    const response = await fetch('https://api.example.com/items');
    items.value = await response.json();
  } catch (e) {
    console.error("Failed to load items", e);
  }
});
</script>

<template>
  <div class="container">
    <h1>Counter: {{ count }}</h1>
    <p>Double: {{ doubleCount }}</p>
    <button @click="increment">Increment</button>

    <ul v-if="items.length">
      <li v-for="item in items" :key="item.id">{{ item.name }}</li>
    </ul>
    <p v-else>Loading items...</p>
  </div>
</template>

<style scoped>
.container {
  padding: 20px;
  font-family: sans-serif;
}
.container h1 {
  color: #42b983;
}
</style>
```

**Complexity**:
- **Time**: Updating a reactive property is $O(1)$; re-rendering the affected component is $O(N)$ where $N$ is the number of DOM nodes in the component.
- **Space**: $O(M)$ where $M$ is the size of the reactive state.

## Interview questions

### Q1: What is the difference between the Options API and the Composition API in Vue 3?
**Model answer**: The Options API organizes code by "options" like `data`, `methods`, and `computed`, which is intuitive for beginners but makes logic reuse difficult in large components. The Composition API allows us to group code by logical feature using the `setup` function, enabling the creation of "Composables" that can be shared across components, similar to React Hooks.

### Q2: How does Nuxt.js improve SEO compared to a standard Vue SPA?
**Model answer**: A standard Vue SPA renders the page in the browser (Client-Side Rendering), meaning search engine bots often see an empty `div` before the JS executes. Nuxt.js provides Server-Side Rendering (SSR), sending a fully populated HTML page to the browser. This allows bots to index the content immediately, significantly improving SEO.

### Q3: What are "Composables" in Vue 3?
**Model answer**: Composables are functions that leverage the Composition API to encapsulate and reuse stateful logic. For example, a `useAuth` composable could handle the user's login state, token storage, and permission checks, and then be imported into any component that needs authentication logic.

### Q4: How does Vue's reactivity system work under the hood?
**Model answer**: In Vue 3, reactivity is implemented using JavaScript `Proxy` objects. When a reactive object is created, Vue wraps it in a Proxy. When a property is accessed, the Proxy's `get` trap is triggered, and Vue "tracks" the current effect. When a property is modified, the `set` trap is triggered, and Vue notifies all "tracked" effects to re-run.

### Q5: When would you choose Nuxt.js over a plain Vue application?
**Model answer**: I would choose Nuxt.js when the project requires strong SEO (e.g., an e-commerce site), fast initial page loads via SSG, or when the project is large enough that file-system routing and auto-imports significantly improve developer productivity.

## Related notes

- [React](../03-frontend/react.md)
- [Next.js](../03-frontend/nextjs.md)
- [Frontend Security](../03-frontend/frontend-security.md)

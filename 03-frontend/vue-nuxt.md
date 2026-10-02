---
title: "Vue.js and Nuxt.js Fundamentals"
tags: ["frontend","vue","nuxt"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Vue and Nuxt.js

## 1. Vue.js Core Concepts

### Reactivity System
Vue uses a proxy-based reactivity system (Vue 3) that automatically tracks dependencies.
- **`ref()`**: For primitive values (returns a wrapper object with `.value`).
- **`reactive()`**: For objects/arrays (returns a proxy).
- **`computed()`**: Derived state that caches results until dependencies change.

### Component Communication
- **Props**: Parent $\rightarrow$ Child (One-way data flow).
- **Emits**: Child $\rightarrow$ Parent (Event-based).
- **Provide/Inject**: Deeply nested communication (similar to React Context).
- **Pinia**: The official state management store (replacement for Vuex).

### Composition API vs Options API
- **Options API**: Organizes code by `data`, `methods`, `computed`. (Good for small components).
- **Composition API**: Organizes code by logical concern using `setup()`. (Better for reuse and TypeScript support).

## 2. Nuxt.js (Vue Framework)

Nuxt provides a layer on top of Vue for production-grade applications, primarily focusing on SEO and Performance.

### Rendering Modes
- **SSR (Server-Side Rendering)**: HTML is generated on the server on every request. (Best for SEO).
- **SSG (Static Site Generation)**: HTML is generated at build time. (Fastest, but content is static).
- **CSR (Client-Side Rendering)**: Standard Vue app; browser renders everything.
- **Hybrid Rendering**: Define different strategies per route (e.g., `/blog` is SSG, `/profile` is SSR).

### Key Features
- **File-based Routing**: Folders in `/pages` automatically become routes.
- **Auto-imports**: Components and composables are automatically imported.
- **Server Engine (Nitro)**: High-performance server that allows deploying to serverless environments (Vercel, Netlify).

## 3. Vue vs React: Interview Comparison

| Feature | React | Vue |
| :--- | :--- | :--- |
| **Reactivity** | Explicit (`useState`, `useEffect`) | Transparent (Proxies, `ref`) |
| **Templates** | JSX (JavaScript-centric) | HTML-based templates (Separation of concerns) |
| **State Management**| Redux, Zustand, Context | Pinia |
| **Learning Curve** | Steeper (requires JS mastery) | Gentler (more intuitive for HTML/CSS devs) |
| **Eco-system** | Massive, fragmented | Integrated (official Router/Store) |

## 4. Common Interview Questions

**Q: What is the "Virtual DOM" and how does Vue use it?**
**A**: A lightweight JS representation of the real DOM. Vue compares the new VDOM with the old one (diffing) and applies only the necessary changes to the real DOM, reducing expensive browser repaints.

**Q: How does `v-if` differ from `v-show`?**
**A**: `v-if` conditionally renders the element (it is added/removed from the DOM). `v-show` merely toggles the `display: none` CSS property. Use `v-if` for rare changes and `v-show` for frequent toggling.

## Related notes

- [React notes](03-frontend/react.md)
- [Browser internals](03-frontend/browser-internals.md)

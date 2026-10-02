---
title: "Micro-frontends and Design Systems"
tags: ["frontend","architecture","design-systems"]
difficulty: hard
status: learning
last_reviewed: 2026-10-02
---

# Micro-frontends and Design Systems

## 1. Micro-frontends Architecture

Micro-frontends extend the microservices concept to the frontend, allowing different teams to own different parts of the UI.

### Implementation Strategies
- **Build-time Integration**: Components are published as npm packages. (Tight coupling, slow deployments).
- **Run-time Integration (Iframes)**: Strict isolation, but poor UX and SEO.
- **Module Federation (Webpack 5)**: The industry standard. Allows an application to dynamically load code from another build at runtime.
- **Shell/Orchestrator**: A "Main" app that handles routing, authentication, and loading the various micro-apps.

### Trade-offs
- **Pros**: Independent deployments, technology agnostic (Vue app inside a React shell), team autonomy.
- **Cons**: Increased bundle size (duplicate libraries), CSS collisions, complex global state management.

## 2. Design Systems

A design system is a single source of truth for UI components, patterns, and brand guidelines.

### Core Layers
1. **Design Tokens**: The smallest atoms (Colors, Spacing, Typography, Shadows). Stored as JSON/CSS variables.
2. **Component Library**: Reusable UI elements (Buttons, Inputs, Modals) built using tokens.
3. **Pattern Library**: Combinations of components to solve a specific task (e.g., "User Profile Header").
4. **Documentation**: Guidelines on *when* and *how* to use the components.

### Implementation Patterns
- **Themed Components**: Use CSS Variables or Theme Providers (React Context) to allow switching between Dark/Light modes.
- **Headless UI**: Creating logic-only components (e.g., Radix UI, Headless UI) and letting the consumer provide the styling. This separates accessibility/logic from visual design.

## 3. Interview Q&A

**Q: How do you handle CSS collisions in a micro-frontend architecture?**
**A**: 
1. **CSS Modules**: Scopes CSS to the component.
2. **BEM Naming**: Strict naming conventions.
3. **Shadow DOM**: True encapsulation provided by Web Components.
4. **Tailwind CSS**: Utility-first approach reduces the need for custom global CSS.

**Q: When should you NOT use micro-frontends?**
**A**: For small to medium teams. The operational overhead (CI/CD complexity, shared dependency management) outweighs the benefits unless you have hundreds of developers across different domains.

## Related notes

- [React notes](03-frontend/react.md)
- [CSS basics](03-frontend/css.md)

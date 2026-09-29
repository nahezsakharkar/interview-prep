---
title: "TypeScript Essentials"
tags: ["languages"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# TypeScript Essentials

## Definition

TypeScript is a statically checked superset of JavaScript that adds a type system and compiles to JavaScript. Types improve development-time checking and API communication; they are erased and do not automatically validate runtime input.

## Why it matters / when to use

TypeScript is common in React, Next.js, and full-stack codebases. It helps model contracts and catch many mistakes before runtime, while external data still requires runtime validation.

## How it works

### `type` and `interface`

Both can describe object shapes. Interfaces support declaration merging and `extends`; type aliases can name unions, intersections, primitives, tuples, and mapped types. Choose based on the shape and API intent, and use one convention consistently within a codebase.

### Generics and narrowing

Generics preserve relationships between input and output types. Control-flow narrowing refines a union after checks such as `typeof`, `in`, equality checks, or a discriminant property. Narrow `unknown` at runtime rather than asserting untrusted values into a type.

### Utility types

Built-in utilities transform existing types: `Pick<T, K>` selects keys, `Omit<T, K>` removes keys, `Partial<T>` makes properties optional, and `Record<K, V>` maps keys to values.

### Runtime boundary

Type annotations are not runtime checks. HTTP responses, JSON, local storage, and other external values should enter as `unknown` and be validated before use. A cast such as `value as User` changes compiler assumptions but does not inspect the value.

## Code example

```ts
type User = {
  id: number;
  name: string;
};

type UserPreview = Pick<User, "id" | "name">;

function isRecord(value: unknown): value is Record<string, unknown> {
  return typeof value === "object" && value !== null && !Array.isArray(value);
}

function parseUser(value: unknown): UserPreview | null {
  if (!isRecord(value)) return null;
  if (typeof value.id !== "number" || !Number.isInteger(value.id)) return null;
  if (typeof value.name !== "string") return null;
  return { id: value.id, name: value.name };
}

function pluck<T, K extends keyof T>(items: readonly T[], key: K): T[K][] {
  return items.map((item) => item[key]);
}

const raw: unknown = JSON.parse('{"id":42,"name":"Asha"}');
const parsed = parseUser(raw);
const names = pluck([{ id: 42, name: "Asha" }], "name");

console.log(parsed?.name, names[0]);
```

The example can be checked with TypeScript 5.x using strict type checking and runs after compilation to JavaScript. Runtime JSON validation is performed by `parseUser`; the `as unknown` annotation does not validate the parsed data.

## Time and space complexity / trade-offs

- Type annotations, generics, and utility types are erased; they do not add runtime cost by themselves.
- `parseUser` checks a fixed number of fields: O(1) time and O(1) extra space for this fixed schema.
- `pluck` visits $n$ elements: O(n) time and O(n) output space.
- Static checking improves feedback and refactoring, but adds compiler/configuration complexity and cannot replace validation at trust boundaries.

## Common mistakes

- Using `any` to silence errors instead of modeling or narrowing the value.
- Assuming interfaces or type aliases validate JSON at runtime.
- Using a type assertion as if it inspected the value.
- Confusing a type union (`A | B`) with JavaScript's runtime logical OR operator.
- Overusing non-null assertions (`!`) instead of handling absent values.
- Choosing `interface` vs `type` by a universal rule; both are useful, with different capabilities.

## Interview questions

### Q1: What is the difference between `type` and `interface`?
**Model answer:** Both describe object shapes. Interfaces can merge declarations and extend other interfaces; type aliases can also represent unions, intersections, primitives, tuples, and mapped types. Team consistency and the specific shape should guide the choice.

### Q2: What is a generic, and when is it useful?
**Model answer:** A generic parameter lets a function or type preserve relationships across input and output types, such as `pluck<T, K extends keyof T>` returning values of the selected property type without losing information.

### Q3: How does control-flow narrowing work?
**Model answer:** TypeScript uses checks in program flow—such as `typeof`, a discriminant, or an `in` check—to refine a broad union to a more specific member within a branch.

### Q4: Do TypeScript types validate API responses at runtime?
**Model answer:** No. Types are erased during compilation. Treat external data as `unknown` and validate its shape at runtime using explicit checks or a schema-validation library.

### Q5: What are utility types? Give examples.
**Model answer:** Utility types transform existing types. `Pick` selects properties, `Omit` removes properties, `Partial` makes properties optional, and `Record` describes a key-to-value mapping.

### Q6: When should you avoid `any`?
**Model answer:** Avoid it when the value can be modeled with a concrete type or safely narrowed from `unknown`. `any` disables useful checking and can spread unsound assumptions through a codebase.

### Q7: What is the difference between a union type and `||`?
**Model answer:** `A | B` is a compile-time type meaning a value may conform to either type. `||` is a runtime JavaScript operator that evaluates operands and returns one based on truthiness.

### Q8: What does TypeScript add to runtime performance?
**Model answer:** Type annotations and most type constructs are erased, so they do not directly execute at runtime. Runtime cost comes from the emitted JavaScript and any validation or helper code actually run.

### Q9: Why is `unknown` safer than `any` for external data?
**Model answer:** `unknown` accepts any input but prevents using it as a specific type until it is narrowed. `any` disables those checks, so mistakes can pass through compilation.

### Q10: What is a discriminated union?
**Model answer:** It is a union of object types that share a literal-valued property, such as `kind`. Checking that property narrows the value to the corresponding member and makes exhaustive handling easier.

## Related topics

- [Java fundamentals](../java/java-fundamentals.md)
- [JavaScript essentials](../javascript/javascript-essentials.md)
- [React interview notes](../../03-frontend/react.md)

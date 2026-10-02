---
title: "React Native Basics"
tags: ["frontend","react-native","mobile"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# React Native Basics

## Definition

React Native is a framework for building native mobile applications using React. Unlike mobile web apps, React Native invokes native platform UI components instead of rendering to a browser DOM.

## Core Concepts

### 1. The Bridge vs. New Architecture (Fabric)
- **The Bridge (Legacy)**: React Native used a JSON-based bridge to communicate between the JavaScript thread and the Native thread. This was asynchronous and could become a bottleneck for high-frequency updates (e.g., animations).
- **Fabric (New)**: The new architecture uses JSI (JavaScript Interface), allowing JS to hold a direct reference to native objects. This enables synchronous communication and significantly improved performance.

### 2. Core Components
React Native provides a set of built-in components that map to native views:

| Web Component | React Native Component | Native Equivalent (iOS/Android) |
| :--- | :--- | :--- |
| `<div>` | `<View>` | `UIView` / `ViewGroup` |
| `<span>` / `<p>` | `<Text>` | `UITextView` / `TextView` |
| `<img>` | `<Image>` | `UIImageView` / `ImageView` |
| `<ul>` / `<li>` | `<FlatList>` / `<ScrollView>` | `UITableView` / `RecyclerView` |
| `<button>` | `<TouchableOpacity>` / `<Pressable>` | `UIButton` / `Button` |

### 3. Styling and Layout
React Native uses a subset of CSS implemented via **Flexbox**. 
- **Default Direction**: The default `flexDirection` is `column` (unlike web, which is `row`).
- **No CSS files**: Styles are typically defined using `StyleSheet.create()`.

## Performance Optimization

1. **FlatList over ScrollView**: Use `FlatList` for long lists. It only renders items currently visible on the screen (virtualization), preventing memory crashes.
2. **Avoid Inline Functions**: Defining functions inside `render()` or as props (e.g., `onPress={() => doSomething()}`) causes the component to re-render on every cycle. Use `useCallback`.
3. **Optimizing Images**: Use specialized libraries like `react-native-fast-image` for better caching and flicker-free loading.
4. **Reducing Bridge Traffic**: Move heavy logic to the native side or use the New Architecture to avoid JSON serialization overhead.

## Working Code Example

This example shows a basic a list of items with a a custom style, demonstrating the use of `FlatList` and `TouchableOpacity`.

```tsx
import React, { useCallback } from 'react';
import { 
  StyleSheet, 
  Text, 
  View, 
  FlatList, 
  TouchableOpacity, 
  SafeAreaView 
} from 'react-native';

const DATA = [
  { id: '1', title: 'Account Balance' },
  { id: '2', title: 'Transaction History' },
  { id: '3', title: 'Investment Portfolio' },
];

const App = () => {
  const renderItem = useCallback(({ item }: { item: { title: string } }) => (
    <TouchableOpacity style={styles.item} onPress={() => console.log(`Pressed ${item.title}`)}>
      <Text style={styles.title}>{item.title}</Text>
    </TouchableOpacity>
  ), []);

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.header}>Financial Dashboard</Text>
      <FlatList
        data={DATA}
        renderItem={renderItem}
        keyExtractor={item => item.id}
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
    marginTop: 20,
  },
  header: {
    fontSize: 24,
    fontWeight: 'bold',
    textAlign: 'center',
    marginVertical: 20,
  },
  item: {
    backgroundColor: '#fff',
    padding: 20,
    marginVertical: 8,
    marginHorizontal: 16,
    borderRadius: 8,
    elevation: 3, // Android shadow
    shadowColor: '#000', // iOS shadow
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
  },
  title: {
    fontSize: 18,
  },
});

export default App;
```

**Complexity**:
- **Time**: `FlatList` rendering is $O(V)$ where $V$ is the number of visible items.
- **Space**: $O(V)$ to maintain the rendered components in memory.

## Interview questions

### Q1: How is React Native different from a mobile web app (PWA)?
**Model answer**: A mobile web app runs inside a browser wrapper and uses HTML/CSS. React Native uses JavaScript to control *native* UI components. This results in significantly better performance, access to native device APIs (camera, biometric auth) without wrappers, and a "truly native" look and feel.

### Q2: Why is `FlatList` preferred over `ScrollView` for large lists?
**Model answer**: `ScrollView` renders all its children at once, which leads to high memory usage and slow initial loads for large datasets. `FlatList` uses "virtualization"—it only renders the items currently visible on the screen and recycles them as the user scrolls, keeping the memory footprint constant.

### Q3: What is the "Bridge" in React Native and why is it being replaced?
**Model answer**: The Bridge is the layer that allows JavaScript to communicate with the Native side via asynchronous JSON messages. It's a bottleneck for high-frequency updates (like 60fps animations). The New Architecture replaces it with JSI (JavaScript Interface), allowing JS to call native methods synchronously.

### Q4: How do you handle different screen sizes in React Native?
**Model answer**: I use a combination of Flexbox for fluid layouts and the `Dimensions` API or `useWindowDimensions` hook to conditionally apply styles based on the screen width (e.g., switching from a single-column to a two-column layout on tablets).

### Q5: How do you optimize performance in a React Native app?
**Model answer**: I focus on three areas: 1) Reducing re-renders using `React.memo` and `useCallback`, 2) optimizing list rendering with `FlatList` and `getItemLayout`, and 3) offloading heavy computations to the native side or using the New Architecture.

## Related notes

- [React](../03-frontend/react.md)
- [Frontend Security](../03-frontend/frontend-security.md)
- [Performance](../03-frontend/performance.md)

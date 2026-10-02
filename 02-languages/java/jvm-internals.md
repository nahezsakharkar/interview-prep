---
title: "JVM Internals"
tags: ["languages","java","jvm"]
difficulty: hard
status: revised
last_reviewed: 2026-10-02
---

# JVM Internals

## Definition

The Java Virtual Machine (JVM) is the engine that enables Java's "Write Once, Run Anywhere" (WORA) capability. It translates Java bytecode into machine-specific instructions and manages the application's memory and execution.

## JVM Architecture

The JVM consists of three main subsystems:

### 1. Class Loader Subsystem
Responsible for loading `.class` files into memory.
- **Loading**: Finds the bytecode.
- **Linking**: Verifies the bytecode, prepares static variables, and resolves symbolic references.
- **Initialization**: Executes static initializers.

### 2. Runtime Data Areas (Memory Model)
The JVM divides memory into different zones:

| Area | Visibility | Lifecycle | Purpose |
| :--- | :--- | :--- | :--- |
| **Method Area** | Shared | JVM Life | Stores class metadata, static variables, and constant pool. |
| **Heap** | Shared | JVM Life | Stores all objects created with `new`. This is the target of GC. |
| **Stack** | Per-thread | Thread Life | Stores local variables and method call frames (LIFO). |
| **PC Register** | Per-thread | Thread Life | Stores the address of the current JVM instruction. |
| **Native Method Stack** | Per-thread | Thread Life | Handles calls to native (C/C++) code via JNI. |

### 3. Execution Engine
- **Interpreter**: Executes bytecode line-by-line (slow start).
- **JIT (Just-In-Time) Compiler**: Identifies "hot spots" (frequently called code) and compiles them directly into native machine code for high performance.
- **Garbage Collector (GC)**: Automatically reclaims memory from unreachable objects.

## Garbage Collection (GC)

### Generational Hypothesis
Most objects die young. Therefore, the Heap is divided into:
1. **Young Generation**:
    - **Eden Space**: Where new objects are born.
    - **Survivor Spaces (S0, S1)**: Objects that survive a "Minor GC" move here.
2. **Old Generation (Tenured)**: Objects that survive enough Minor GCs are promoted here. "Major GC" or "Full GC" cleans this area.

### GC Algorithms
- **Serial GC**: Single-threaded; stops the world (STW). Used for small apps.
- **Parallel GC**: Multi-threaded for Young Gen. Default in Java 8.
- **G1 (Garbage First)**: Divides the heap into regions. Prioritizes regions with the most garbage. Default in Java 9+.
- **ZGC / Shenandoah**: Ultra-low latency collectors that perform most work concurrently with the application threads.

## Java Memory Model (JMM)

The JMM defines how threads interact through memory.
- **Visibility**: Changes made by one thread to a variable might not be visible to others due to CPU caching.
- **`volatile` keyword**: Ensures a variable is read from and written directly to main memory, guaranteeing visibility across threads.
- **`synchronized` / `Lock`**: Ensures mutual exclusion (only one thread can access a block of code) and prevents race conditions.

## Working Code Example: Memory Leak Simulation

This example demonstrates how a "forgotten" reference in a static collection can prevent the GC from reclaiming memory, leading to an `OutOfMemoryError`.

```java
import java.util.*;

public class MemoryLeakDemo {
    // Static collection: lives for the entire life of the JVM
    private static final List<byte[]> LEAK_LIST = new ArrayList<>();

    public static void main(String[] args) {
        while (true) {
            // Create a large object and add it to the static list
            byte[] data = new byte[1024 * 1024]; // 1MB
            LEAK_LIST.add(data); 
            // The GC cannot reclaim 'data' because it's still referenced by LEAK_LIST
            System.out.println("Current leak size: " + LEAK_LIST.size() + " MB");
        }
    }
}
```
**Complexity**: Time $O(1)$ per iteration; Space $O(n)$ where $n$ is the number of iterations until `OutOfMemoryError` occurs.

## Interview questions

### Q1: Explain the difference between the Stack and the Heap.
**Model answer**: The Stack is used for static memory allocation and thread-execution. It stores local variables and method frames in a LIFO order; it is fast and automatically managed. The Heap is used for dynamic memory allocation for objects. It is shared across all threads and is managed by the Garbage Collector.

### Q2: What is the "Stop-the-World" (STW) event?
**Model answer**: An STW event occurs when the Garbage Collector pauses all application threads to safely move objects or update references in the heap. Minimizing STW pauses is the primary goal of modern collectors like G1 and ZGC.

### Q3: How does the JIT compiler improve performance?
**Model answer**: The JIT compiler monitors the code as it runs. When it detects a "hot spot" (a method called thousands of times), it compiles that bytecode into native machine code. Subsequent calls execute the native code directly, bypassing the interpreter and significantly increasing speed.

### Q4: What is the difference between a Minor GC and a Full GC?
**Model answer**: A Minor GC cleans the Young Generation (Eden and Survivor spaces). It is frequent and fast. A Full GC cleans the entire heap, including the Old Generation. It is much slower and usually involves a longer STW pause.

### Q5: How do you detect and fix a memory leak in Java?
**Model answer**: I use a profiler (e.g., VisualVM or JProfiler) to analyze a **Heap Dump**. I look for "dominant" objects or collections that grow indefinitely. Once the leak is found, I fix it by removing the static reference or using a `WeakHashMap` for caches.

## Related notes

- [Java Fundamentals](../02-languages/java/java-fundamentals.md)
- [Spring Boot internals](../04-backend/spring-boot-internals.md)

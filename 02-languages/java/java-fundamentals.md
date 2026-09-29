---
title: "Java Fundamentals"
tags: ["languages"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Java Fundamentals

Tags: #java #oop
Difficulty: Medium
Status: Learning

## Definition

Java is a strongly typed, object-oriented language that emphasizes readability, portability, and JVM-based runtime behavior.

## Why it matters / when to use

Java is widely used in enterprise applications and backend systems. Interviewers often test fundamentals like collections, generics, OOP, and concurrency basics.

## How it works

Key areas include class design, inheritance, interfaces, exception handling, generics, and the Java collections framework.

## Code example

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");

        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

## Time and space complexity

| Operation | Typical time | Typical space |
| --- | --- | --- |
| ArrayList get | O(1) | O(1) |
| HashMap get | O(1) average | O(n) |
| TreeSet insert | O(log n) | O(n) |

## Common mistakes and pitfalls

- Confusing checked and unchecked exceptions
- Using raw types instead of generics
- Overusing inheritance when composition is cleaner

## Interview questions

### Q: Why use interface-based design?
Model answer: It reduces coupling, makes the implementation replaceable, and supports multiple implementations behind the same contract.

## Related topics

- [TypeScript essentials](../../02-languages/typescript/typescript-essentials.md)
- [JavaScript essentials](../../02-languages/javascript/javascript-essentials.md)
- [Spring Boot essentials](../../04-backend/spring-boot.md)

---
title: "Java Collections and Internals"
tags: ["languages","java","collections"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Java Collections and Internals

## Definition

The Java Collections Framework (JCF) is a set of classes and interfaces that provide a standardized way to handle groups of objects. Understanding the internal workings of these collections is critical for optimizing performance in backend systems.

## 1. List Implementations

### ArrayList
- **Structure**: Dynamic array.
- **Time Complexity**: `get(i)` is $O(1)$; `add()` is $O(1)$ amortized; `remove(i)` is $O(n)$ due to shifting.
- **Internals**: When the array is full, it creates a new array (usually 1.5x size) and copies the elements.

### LinkedList
- **Structure**: Doubly linked list.
- **Time Complexity**: `get(i)` is $O(n)$; `add()` is $O(1)$ if adding at the ends.
- **Use Case**: Efficient for frequent insertions/deletions at the ends.

## 2. Map Implementations (The "Interview Favorite")

### HashMap Internals
A `HashMap` uses a hash table to store key-value pairs.

**How it works**:
1. **Hashing**: The key's `hashCode()` is used to calculate an index in an internal array (buckets).
2. **Bucket Collision**: If two keys hash to the same index, they are stored in a **Linked List** (or a **Red-Black Tree** if the list size exceeds 8 in Java 8+).
3. **Retrieval**: The map finds the bucket via hash and then iterates through the list/tree using `.equals()` to find the exact key.

**Complexity**:
- Average case: $O(1)$ for `put` and `get`.
- Worst case: $O(\log n)$ if many keys collide (due to the Red-Black Tree).

### TreeMap
- **Structure**: Red-Black Tree (Sorted Map).
- **Complexity**: $O(\log n)$ for all basic operations.
- **Use Case**: When you need the keys to be sorted.

## 3. Set Implementations

### HashSet
A `HashSet` is internally just a `HashMap` where the value is a dummy constant. It ensures uniqueness by leveraging the `HashMap`'s key uniqueness.

## 4. Comparison Table

| Collection | Ordered? | Sorted? | Nulls Allowed? | Time (Avg) |
| :--- | :--- | :--- | :--- | :--- |
| **ArrayList** | Yes | No | Yes | $O(1)$ access |
| **LinkedList** | Yes | No | Yes | $O(n)$ access |
| **HashSet** | No | No | Yes | $O(1)$ lookup |
| **TreeSet** | No | Yes | No | $O(\log n)$ lookup |
| **HashMap** | No | No | Yes | $O(1)$ lookup |
| **TreeMap** | No | Yes | No | $O(\log n)$ lookup |

## Working Code Example: Custom Key for HashMap

To use a custom object as a `HashMap` key, you **must** override both `hashCode()` and `equals()`. If you only override one, the map will fail to find your object.

```java
import java.util.*;

class User {
    private final int id;
    private final String name;

    public User(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        User user = (User) o;
        return id == user.id && Objects.equals(name, user.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }

    public String getName() { return name; }
}

public class MapTest {
    public static void main(String[] args) {
        Map<User, String> userRoles = new HashMap<>();
        User u1 = new User(1, "Alice");
        userRoles.put(u1, "Admin");

        // This works because we overrode hashCode and equals
        System.out.println(userRoles.get(new User(1, "Alice"))); // Admin
    }
}
```

**Complexity**: `Objects.hash()` takes $O(1)$ time. The `HashMap` lookup is $O(1)$ average.

## Interview questions

### Q1: Why is the `hashCode()` and `equals()` contract important?
**Model answer**: If two objects are equal according to `equals()`, they must produce the same `hashCode()`. If they don't, the `HashMap` will look in the wrong bucket and fail to find the object, even if it's logically present.

### Q2: What happens during a HashMap resize?
**Model answer**: When the number of elements exceeds the `loadFactor` (default 0.75), the map doubles its internal array size. Every existing element is then re-hashed and moved to a new bucket. This is an $O(n)$ operation.

### Q3: Difference between `ArrayList` and `Vector`?
**Model answer**: `Vector` is synchronized (thread-safe), which makes it slower. `ArrayList` is not synchronized. For thread-safety, use `CopyOnWriteArrayList` or `Collections.synchronizedList()`.

### Q4: How does a `TreeMap` maintain order?
**Model answer**: It uses a Red-Black Tree, a self-balancing binary search tree. This ensures that the height of the tree is always $O(\log n)$, keeping operations efficient while keeping keys sorted.

### Q5: When would you use a `LinkedList` over an `ArrayList`?
**Model answer**: Only when you have a very high volume of insertions or deletions at the head/tail of the list. For almost all other cases (especially random access), `ArrayList` is significantly faster due to CPU cache locality.

## Related notes

- [JVM Internals](../02-languages/java/jvm-internals.md)
- [Java Fundamentals](../02-languages/java/java-fundamentals.md)
- [Spring Boot internals](../04-backend/spring-boot-internals.md)

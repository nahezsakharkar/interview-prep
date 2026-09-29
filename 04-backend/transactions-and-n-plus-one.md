---
title: "Transactions and N+1"
tags: ["backend","database","performance"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Transactions and N+1

## Transactions

A transaction groups multiple operations so they are either all committed or all rolled back. In Spring, this is often controlled using `@Transactional`.

### Key properties

- Atomicity
- Consistency
- Isolation
- Durability

## N+1 problem

The N+1 problem happens when a parent query returns N rows and then the application performs N more queries to fetch related data. This creates a large number of DB round trips.

## Example

```java
List<User> users = userRepository.findAll();
for (User user : users) {
    System.out.println(user.getOrders().size());
}
```

This can become a hidden performance bottleneck when each `user.getOrders()` triggers a separate query.

## Fixes

- Fetch join or batch fetch related data
- Use pagination where large datasets are involved
- Keep transaction boundaries tight
- Use query projections when only limited fields are needed

## Interview guidance

- Transactions protect correctness under failure.
- N+1 is a read-performance issue, not a correctness issue.
- Always reason about whether the read pattern scales with real data volume.

## Related notes

- [Spring Boot internals](spring-boot-internals.md)
- [REST design](rest-design.md)
- [JWT and OAuth2](jwt-oauth2.md)

---
title: "Spring Boot Deep Dive: Security and JPA"
tags: ["backend","spring-boot","security","jpa"]
difficulty: hard
status: revised
last_reviewed: 2026-10-02
---

# Spring Boot Deep Dive: Security and JPA

## 1. Spring Security Internals

Spring Security is essentially a chain of **Servlet Filters**.

### The Filter Chain
When a request hits the server, it passes through the `FilterChainProxy`, which manages a list of `SecurityFilterChain`s.
1. **Authentication Filter**: Extracts credentials (e.g., JWT from header).
2. **Authentication Manager**: Validates credentials against a `UserDetailsService` or an external IDP.
3. **Security Context**: If successful, the authenticated user is stored in the `SecurityContextHolder`.
4. **Authorization Filter**: Checks if the current user has the required roles/permissions for the endpoint.

### Common Security Patterns
- **Stateless Auth**: Using JWTs. The server does not store sessions; it validates the token signature on every request.
- **Method-Level Security**: Using `@PreAuthorize("hasRole('ADMIN')")` to protect specific service methods.

## 2. Spring Data JPA and Hibernate

JPA (Java Persistence API) is a specification; Hibernate is the most common implementation.

### The Persistence Context (First-Level Cache)
Hibernate manages a `Session` (Persistence Context). When you fetch an entity, it's stored in this cache.
- If you request the same entity again in the same transaction, Hibernate returns the cached version without a DB call.
- Changes to the entity are automatically synchronized with the DB at the end of the transaction (Dirty Checking).

### The N+1 Problem
This occurs when you fetch a list of entities, and then for each entity, Hibernate executes another query to fetch its related children.

**Example**: Fetching 10 Orders $\rightarrow$ Hibernate runs 1 query for orders + 10 queries for the items in each order = 11 queries.

**Mitigation**:
- **Join Fetch**: Use `JOIN FETCH` in JPQL to load the related entities in a single query.
- **Entity Graphs**: Define which attributes should be eagerly loaded for specific use cases.

### Transaction Management
`@Transactional` ensures that a series of DB operations are atomic.
- **Propagation**: Defines how transactions behave if another transaction is already running (e.g., `REQUIRED` starts a new one or joins existing).
- **Isolation Levels**: Controls how transactions see changes made by others (e.g., `READ_COMMITTED` prevents reading uncommitted data).

## Working Code Example: Solving the N+1 Problem

This example shows the difference between a naive fetch and an optimized fetch.

```java
// NAIVE: Causes N+1 problem
@Query("SELECT o FROM Order o")
List<Order> findAllOrders();

// OPTIMIZED: Solves N+1 using JOIN FETCH
@Query("SELECT o FROM Order o JOIN FETCH o.items")
List<Order> findAllOrdersWithItems();
```

**Complexity**:
- **Naive**: $O(1 + N)$ queries.
- **Optimized**: $O(1)$ query.

## Interview questions

### Q1: How does `@Transactional` work under the hood?
**Model answer**: Spring uses **AOP (Aspect Oriented Programming)**. It creates a proxy around the bean. When the method is called, the proxy starts a transaction, executes the method, and then commits (or rolls back on exception) the transaction.

### Q2: What is the difference between `L1` and `L2` cache in Hibernate?
**Model answer**: The L1 cache is the Session-level cache; it's mandatory and only lasts for the duration of the transaction. The L2 cache is a shared cache across sessions (e.g., using Ehcache or Redis) and can persist across transactions.

### Q3: How do you handle optimistic locking in JPA?
**Model answer**: Use the `@Version` annotation on a field (usually an integer). Hibernate checks the version before updating. If the version in the DB has changed since the entity was loaded, a `OptimisticLockException` is thrown.

### Q4: Difference between `FetchType.LAZY` and `FetchType.EAGER`?
**Model answer**: `EAGER` loads the relationship immediately. `LAZY` loads it only when first accessed. `LAZY` is generally preferred to avoid loading massive amounts of unnecessary data.

### Q5: How does Spring Security handle a failed authentication?
**Model answer**: The `AuthenticationManager` throws an `AuthenticationException`. This is caught by the `ExceptionTranslationFilter`, which then triggers the `AuthenticationEntryPoint` to return a 401 Unauthorized response.

## Related notes

- [Spring Boot internals](../04-backend/spring-boot-internals.md)
- [Transactions and N+1](../04-backend/transactions-and-n-plus-one.md)
- [JWT and OAuth2](../04-backend/jwt-oauth2.md)

---
title: "Spring Boot internals"
tags: ["backend","spring-boot","java"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Spring Boot internals

## What Spring Boot is doing

Spring Boot reduces boilerplate and bootstraps an application with sensible defaults. Internally, it wires dependencies via Spring's IoC container and auto-configuration.

## IoC and DI

- IoC: the framework controls object creation and wiring
- DI: dependencies are injected rather than manually constructed
- `@Component`, `@Service`, `@Repository`, `@Configuration` register beans

## Bean lifecycle

1. Bean definition is discovered
2. Bean instantiated
3. Dependencies injected
4. Post-processing / initialization hooks run
5. Bean is used in the application context
6. Shutdown hooks run when the container closes

## Auto-configuration

Spring Boot inspects the classpath and activates configuration classes such as `DataSourceAutoConfiguration` or `WebMvcAutoConfiguration` based on present dependencies.

## Example

```java
@SpringBootApplication
public class DemoApp {
    public static void main(String[] args) {
        SpringApplication.run(DemoApp.class, args);
    }
}
```

## Interview guidance

- Prefer constructor injection for immutability and testability.
- Understand the difference between `@Service`, `@Component`, and `@Configuration`.
- Explain why auto-configuration reduces manual setup while still being overrideable.

## Related notes

- [REST design](rest-design.md)
- [JWT and OAuth2](jwt-oauth2.md)
- [Transactions and N+1](transactions-and-n-plus-one.md)

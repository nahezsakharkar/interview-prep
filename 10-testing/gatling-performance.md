---
title: "Performance Testing with Gatling"
tags: ["testing","performance","gatling"]
difficulty: hard
status: revised
last_reviewed: 2026-10-02
---

# Performance Testing with Gatling

## Definition

Gatling is a high-performance load testing tool built on Akka and Netty. Unlike JMeter, which uses one thread per user (limiting scalability), Gatling uses an **asynchronous, non-blocking architecture**, allowing a single machine to simulate thousands of concurrent users.

## Core Concepts

### 1. Simulation
A simulation is a script that describes the behavior of a user. It includes:
- **HTTP Protocol**: The base URL and headers.
- **Scenario**: A sequence of actions (e.g., `Login` $\rightarrow$ `Search` $\rightarrow$ `Checkout`).
- **Injection Profile**: How users are introduced to the system (e.g., "Ramp up 100 users over 2 minutes").

### 2. Virtual Users (VUs)
Gatling doesn't use threads for VUs. Instead, it uses an event-driven model. When a request is sent, Gatling doesn't block; it registers a callback for when the response arrives. This is why Gatling can simulate $10,000$ users on a laptop where JMeter would crash.

### 3. Feeders
Feeders are used to inject dynamic data into tests (e.g., a CSV file with 1,000 different user accounts) to avoid caching effects and simulate real-world usage.

## Working Code Example: Load Test Scenario

This example (in Scala/Java DSL) defines a scenario that tests the laentcy of the la-Payment API under load.

```scala
import io.gatling.core.Predef._
import io.gatling.http.Predef._
import scala.concurrent.duration._

class PaymentLoadTest extends Simulation {

  // 1. Define HTTP Protocol
  val httpProtocol = http.baseUrl("https://api.payments.com")
    .acceptHeader("application/json")

  // 2. Define the Scenario
  val scn = scenario("Payment Checkout Flow")
    .exec(http("Request Payment")
      .post("/payment/create")
      .body(StringBody("""{"amount": 100, "currency": "USD"}""")).asJson
      .check(status.is(201)))
    .pause(2.seconds)
    .exec(http("Verify Status")
      .get("/payment/status/123")
      .check(jsonPath("$.status").is("SUCCESS")))

  // 3. Define the Injection Profile
  setUp(
    scn.inject(
      rampUsers(100) during (1.minute), // Gradual increase
      constantUsersPerSec(10) during (5.minutes) // Steady state
    )
  ).protocols(httpProtocol)
}
```

**Complexity**:
- **Time**: Execution is $O(S)$ where $S$ is the total number of simulated requests.
- **Space**: $O(V)$ where $V$ is the number of virtual users (very low due to non-blocking I/O).

## Performance Metrics to Track

| Metric | Definition | Ideal Value |
| :--- | :--- | :--- |
| **Throughput** | Requests per second (RPS) the system can handle | Higher is better |
| **Latency (p95)** | The response time for the fastest 95% of requests | Lower is better |
| **Error Rate** | % of requests that resulted in 4xx or 5xx | $< 0.1\%$ |
| **Saturation** | CPU/Memory usage of the server during peak load | $\approx 70-80\%$ |

## Interview questions

### Q1: Why choose Gatling over JMeter?
**Model answer**: Scalability. JMeter uses a thread-per-user model, which consumes massive amounts of memory as the number of users grows. Gatling uses an asynchronous, event-driven architecture (Akka), allowing it to simulate thousands of users on a single machine with very low resource overhead.

### Q2: What is a "Ramp-up" period and why is it important?
**Model answer**: A ramp-up is the period where users are gradually added to the system. This is important because a "spike" of 1,000 users hitting a system at second zero can cause artificial crashes (e.g., connection pool exhaustion) that don't represent real-world growth.

### Q3: How do you handle "dynamic data" in a performance test?
**Model answer**: I use **Feeders**. Instead of using one test user for 1,000 requests (which would be cached by the DB), I provide a CSV file with 1,000 unique users. Gatling picks a new user for each iteration, ensuring the test hits different database rows and cache buckets.

### Q4: What is the difference between "Stress Testing" and "Load Testing"?
**Model answer**: Load testing checks if the system can handle the *expected* peak traffic (e.g., 1k RPS) while maintaining SLAs. Stress testing pushes the system *beyond* its limits to find the breaking point (e.g., "at what RPS does the DB crash?") and to see how the system recovers from failure.

### Q5: How do you interpret a p99 latency spike?
**Model answer**: A p99 spike means the slowest 1% of users are experiencing significant delays. This is often caused by "Stop-the-World" GC pauses in Java, TCP re-transmissions, or cold-starts of serverless functions. I investigate these by correlating the spike with system metrics like GC logs and CPU usage.

## Related notes

- [Testing Pyramid](../10-testing/test-pyramid.md)
- [System Design Case: Payments](../06-system-design/case-study-payments.md)
- [JVM Internals](../02-languages/java/jvm-internals.md)

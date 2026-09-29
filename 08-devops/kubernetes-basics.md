---
title: "Kubernetes Basics"
tags: ["devops"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

 Kubernetes Basics

Tags: #kubernetes #devops
Difficulty: Medium
Status: Learning

## Definition

Kubernetes orchestrates containerized workloads across a cluster and manages deployment, scaling, and recovery.

## Why it matters / when to use

It is the standard for managing containers in production-grade distributed systems.

## How it works

Pods run application containers, Deployments manage replicas, Services provide stable networking, and Ingress handles external access.

## Code example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: app
  template:
    metadata:
      labels:
        app: app
    spec:
      containers:
      - name: app
        image: my-app:latest
```

## Time and space complexity

Operational complexity is dominated by cluster topology, scheduling, and service coordination, not algorithmic complexity.

## Common mistakes and pitfalls

- Ignoring readiness and liveness probes
- Forgetting resource requests and limits
- Treating the cluster as a single node by default

## Interview questions

### Q: What is the difference between a Pod and a Service?
Model answer: A Pod is a unit of workload; a Service provides a stable network endpoint to route traffic to matching Pods.

## Related topics

- [Docker fundamentals](docker.md)
- [Monitoring and observability](monitoring.md)
- [CI/CD principles](ci-cd.md)

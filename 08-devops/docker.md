---
title: "Docker Fundamentals"
tags: ["devops"]
difficulty: easy
status: learning
last_reviewed: 2026-09-30
---

 Docker Fundamentals

Tags: #docker #devops
Difficulty: Medium
Status: Learning

## Definition

Docker packages applications and dependencies into containers that run consistently across environments.

## Why it matters / when to use

It helps with reproducibility, deployment consistency, and local testing of service stacks.

## How it works

Images define runtime state, containers are running instances, and Docker networking/volumes allow communication and persistence.

## Code example

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "run", "dev"]
```

## Time and space complexity

Operationally, Docker reduces deployment variance more than it changes algorithmic complexity.

## Common mistakes and pitfalls

- Using large images unnecessarily
- Ignoring container lifecycle and logs
- Not managing secrets properly

## Interview questions

### Q: How is Docker different from a VM?
Model answer: Containers share the host OS kernel and are lighter-weight, while VMs virtualize a full operating system and usually consume more resources.

## Related topics

- [Git workflow essentials](git.md)
- [Kubernetes basics](kubernetes-basics.md)
- [CI/CD principles](ci-cd.md)

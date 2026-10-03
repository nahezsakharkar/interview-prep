---
title: "Quant Fundamentals"
tags: ["aptitude","math"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Quant Fundamentals

## Definition

Quant fundamentals cover the mathematical reasoning required for aptitude tests, focusing on percentages, ratios, probability, and time-speed-distance problems. The goal is not complex calculus, but rapid, accurate arithmetic reasoning.

## Core Topics and Patterns

### 1. Percentages and Ratios
- **Percentage Change**: $\text{Change} = \frac{\text{New} - \text{Old}}{\text{Old}} \times 100$
- **Ratios**: Expressing a relationship as $a:b$. To find a specific value, find the "unit value" by dividing the total by the sum of ratio parts.

### 2. Probability and Combinatorics
- **Basic Probability**: $P(A) = \frac{\text{Favorable Outcomes}}{\text{Total Outcomes}}$
- **Permutations (Order matters)**: $P(n, r) = \frac{n!}{(n-r)!}$
- **Combinations (Order doesn't matter)**: $C(n, r) = \frac{n!}{r!(n-r)!}$
- **Expected Value**: $E[X] = \sum (x_i \cdot p_i)$. Critical for risk assessment in financial services.

### 3. Time, Speed, and Distance
- **Fundamental**: $\text{Distance} = \text{Speed} \times \text{Time}$
- **Average Speed**: $\text{Total Distance} / \text{Total Time}$. (Warning: Never average the speeds directly).
- **Relative Speed**:
    - Same direction: $S_1 - S_2$
    - Opposite direction: $S_1 + S_2$

### 4. Work and Time
- **Work Rate**: If A does a job in $X$ days and B in $Y$ days, together they do it in $\frac{XY}{X+Y}$ days.

## Working Code Example: Probability Calculator

This TypeScript helper calculates the probability of "at least one" success in $n$ trials, a common pattern in reliability testing.

```ts
/**
 * Calculates the probability of at least one success in n independent trials.
 * Formula: 1 - (probability of failure)^n
 */
function probabilityAtLeastOne(pSuccess: number, nTrials: number): number {
  if (pSuccess < 0 || pSuccess > 1) {
    throw new Error("Probability must be between 0 and 1");
  }
  const pFailure = 1 - pSuccess;
  return 1 - Math.pow(pFailure, nTrials);
}

// Example: Probability of at least one server failing in a 3-node cluster 
// if each has a 1% chance of failure.
const pFail = 0.01;
const nodes = 3;
console.log(`Prob of at least one failure: ${probabilityAtLeastOne(pFail, nodes).toFixed(4)}`);
// Output: 0.0297
```

**Complexity**:
- **Time**: $O(1)$ (using `Math.pow`).
- **Space**: $O(1)$.

## Interview questions

### Q1: A train 150m long passes a pole in 15 seconds. How long will it take to pass a platform 300m long?
**Model answer**: 
1. **Find Speed**: $\text{Speed} = \frac{\text{Distance}}{\text{Time}} = \frac{150}{15} = 10\text{ m/s}$.
2. **Total Distance to cross platform**: $\text{Train length} + \text{Platform length} = 150 + 300 = 450\text{m}$.
3. **Time**: $\text{Time} = \frac{\text{Distance}}{\text{Speed}} = \frac{450}{10} = 45\text{ seconds}$.

### Q2: You have 3 red balls and 2 blue balls in a bag. What is the probability of picking 2 balls of the same color?
**Model answer**: 
Total ways to pick 2 balls: $C(5, 2) = \frac{5 \times 4}{2 \times 1} = 10$.
Ways to pick 2 red: $C(3, 2) = 3$.
Ways to pick 2 blue: $C(2, 2) = 1$.
Total favorable outcomes: $3 + 1 = 4$.
$\text{Probability} = \frac{4}{10} = 0.4 \text{ or } 40\%$.

### Q3: If 5 people can build a wall in 12 days, how many days will it take 3 people to build the same wall?
**Model answer**:
Total work = $\text{People} \times \text{Days} = 5 \times 12 = 60\text{ man-days}$.
Days for 3 people = $\frac{60}{3} = 20\text{ days}$.

## Related notes

- [Operating systems](../13-cs-fundamentals/os.md)
- [Networking](../13-cs-fundamentals/networking.md)

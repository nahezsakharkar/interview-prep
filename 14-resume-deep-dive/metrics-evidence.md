---
title: "Resume Metrics Evidence Checklist"
tags: ["resume","metrics","interview-prep"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Resume Metrics Evidence Checklist

## Definition

A defensible resume metric is a precisely defined measurement with a baseline, a result, a scope/time window, a traceable source, and a fair account of attribution and limitations.

## Current Metric Mappings

Based on the project deep-dives, the supplied metrics are tentatively mapped as follows. **All measurement methods remain `(fill in)` until verified by the candidate.**

| Resume value | Project / bullet | Definition and unit | Baseline and result | Period and source | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 60% | KAIZEN Migration | Bundle size reduction or dev velocity | Baseline: X $\rightarrow$ Result: 60% reduction | (fill in) | Pending verification |
| 45% | JSP/Flash Mod | Load time reduction | Baseline: X $\rightarrow$ Result: 45% faster | (fill in) | Pending verification |
| 85% | Admin Panel | Operational efficiency / Ticket reduction | Baseline: X $\rightarrow$ Result: 85% reduction | (fill in) | Pending verification |
| 4x | KaizenLang DSL | Rule change cycle time | Baseline: 3 days $\rightarrow$ Result: 4x faster | (fill in) | Pending verification |
| 300+ tests | Automation Framework | Unique test cases in the suite | Count: 300+ | (fill in) | Pending verification |
| 120+ users | Admin Panel | Total internal operators served | User count: 120+ | (fill in) | Pending verification |

## Evidence Record (Fill-in)

For each metric above, the following details must be collected:

- **Baseline**: What was the exact value before the project started?
- **Formula**: `(Baseline - Final) / Baseline * 100` or similar.
- **Source**: Which tool provided the data? (e.g., Lighthouse, Jira, Google Analytics, Jenkins).
- **Period**: Over what timeframe was this measured?
- **Attribution**: Was this a result of your specific change, or a general team effort?

## Working code example

This helper is used to ensure that percentage claims are mathematically sound.

```ts
function calculateImprovement(baseline: number, final: number, lowerIsBetter: boolean = true): string {
  if (baseline === 0) throw new Error("Baseline cannot be zero");
  
  const diff = lowerIsBetter 
    ? ((baseline - final) / baseline) * 100 
    : ((final - baseline) / baseline) * 100;
    
  return `${diff.toFixed(2)}% improvement`;
}

// Example: Load time went from 5s to 2.75s
console.log(calculateImprovement(5, 2.75)); // "45.00% improvement"
```

## Common mistakes

- **Relative vs Absolute**: Claiming "85% faster" when the baseline was only 1 second (a marginal gain) vs. 10 seconds (a huge gain).
- **Attribution Bias**: Taking 100% credit for a 4x speedup that was actually caused by a backend API optimization you didn't work on.
- **Counting "Runs" as "Tests"**: Claiming "300+ tests" when it's actually 10 tests run 30 times.

## Related notes

- [Resume deep-dive index](README.md)
- [Behavioral STAR method](../11-behavioral-hr/star-method.md)
- [Mistakes log](../99-revision/mistakes-log.md)

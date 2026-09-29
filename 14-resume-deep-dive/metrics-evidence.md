---
title: "Resume Metrics Evidence Checklist"
tags: ["resume","metrics","interview-prep"]
difficulty: medium
status: learning
last_reviewed: 2026-09-30
---

# Resume Metrics Evidence Checklist

> **Evidence boundary:** The supplied resume profile lists `60%`, `45%`, `85%`, `4x`, `300+ tests`, and `120+ users`. It does not map these values to project bullets or provide definitions, baselines, data sources, periods, or attribution. None should be assigned to a project or presented as defensible until the candidate supplies evidence.

## Definition

A defensible resume metric is a precisely defined measurement with a baseline, a result, a scope/time window, a traceable source, and a fair account of attribution and limitations.

## Why it matters / when to use

Interviewers may ask how a claimed percentage, multiplier, test count, or user count was calculated. Clear evidence avoids confusing relative change with absolute values, test runs with unique tests, or team results with individual contribution.

## How it works

For every number, record:

1. The exact resume bullet/project it supports — `> TODO: verify`.
2. Metric definition and unit — `> TODO: verify`.
3. Baseline and final value, with calculation — `> TODO: verify`.
4. Measurement window, population, and exclusions — `> TODO: verify`.
5. Source of truth and reproducibility — `> TODO: verify`.
6. Your contribution and other contributors — `> TODO: verify`.
7. Caveats, uncertainty, and what the metric does not prove — `> TODO: verify`.

## Current unassigned values

| Resume value | Project / bullet | Definition and unit | Baseline and result | Period and source | Status |
| --- | --- | --- | --- | --- | --- |
| 60% | > TODO: verify | > TODO: verify | > TODO: verify | > TODO: verify | Unassigned; do not claim yet |
| 45% | > TODO: verify | > TODO: verify | > TODO: verify | > TODO: verify | Unassigned; do not claim yet |
| 85% | > TODO: verify | > TODO: verify | > TODO: verify | > TODO: verify | Unassigned; do not claim yet |
| 4x | > TODO: verify | > TODO: verify | > TODO: verify | > TODO: verify | Unassigned; do not claim yet |
| 300+ tests | > TODO: verify | Unique tests vs executions: > TODO: verify | > TODO: verify | > TODO: verify | Unassigned; do not claim yet |
| 120+ users | > TODO: verify | Registered / active / unique / other: > TODO: verify | > TODO: verify | > TODO: verify | Unassigned; do not claim yet |

## Working code example

This runnable TypeScript helper calculates a percentage reduction from two non-negative measurements. The sample inputs are **synthetic arithmetic examples**, not the candidate's metrics. The function rejects invalid baselines and non-finite values.

```ts
function percentReduction(baseline: number, after: number): number {
  if (!Number.isFinite(baseline) || baseline <= 0) {
    throw new RangeError("baseline must be finite and greater than zero");
  }
  if (!Number.isFinite(after) || after < 0) {
    throw new RangeError("after must be finite and non-negative");
  }

  return ((baseline - after) / baseline) * 100;
}

console.log(percentReduction(100, 80).toFixed(2));
```

Expected output for this **synthetic example**: `20.00`. Formatting is for display only; retain the underlying values and formula for explanation.

Complexity: time $O(1)$, extra space $O(1)$. The formula is suitable only when a lower `after` value is genuinely an improvement and both measurements use the same definition, unit, and scope.

## Trade-offs and interpretation

- A percentage change needs a meaningful non-zero baseline; small baselines can make percentages look large.
- A multiplier needs numerator/denominator direction stated explicitly, e.g. “4x as many” versus “fourfold reduction in time.”
- A test count needs a counting rule: unique cases, parameterized cases, or executions are not interchangeable.
- A user count needs a definition and time window; registrations are not equivalent to active users.
- Attribution should describe team context and the candidate's actual contribution, not overstate sole ownership.
- Do not round away uncertainty or report a metric without its scope and source.

## Common mistakes

- Assigning a supplied metric to a project based on guesswork.
- Reporting a percentage without defining the baseline, denominator, time period, or population.
- Confusing percentage points with percent change.
- Calling repeated test runs “tests” without explaining the count.
- Treating registered users as monthly or daily active users.
- Taking sole credit for a team result or implying causation from correlation.

## Interview questions and model-answer scaffolds

1. **Which project does this metric describe?** — “It belongs to **[verified resume bullet]**; the source tying it to that project is **[evidence]**.”
2. **What exactly does the percentage measure?** — “It measures **[defined outcome]** over **[scope/time window]**, using **[formula]**.”
3. **What was the baseline?** — “The baseline was **[value/unit/period]**, taken from **[source]**; the comparison used the same definition.”
4. **How did you calculate the change?** — “I compared **[before]** with **[after]** using **[calculation]**; assumptions/exclusions were **[facts]**.”
5. **How do you know the result was reliable?** — “I checked **[data source/repeatability/sample]** and considered **[limitations]**.”
6. **What did you personally contribute?** — “I was responsible for **[specific actions]**; the broader result involved **[team/context]**.”
7. **What does the metric not tell us?** — “It does not establish **[limit]**; the additional evidence needed is **[source/measure]**.”
8. **How was the 4x value defined?** — “The numerator was **[verified quantity]**, denominator **[verified baseline]**, over **[period]**; project mapping remains **[fill in]**.”
9. **What does 300+ tests count?** — “It counts **[unique cases/runs/other]** in **[scope]**, identified from **[test inventory/report]**.”
10. **What does 120+ users mean?** — “It counts **[registered/active/unique definition]** during **[window]**, from **[source]**.”

## Fill-in evidence record

- Resume bullet/project: > TODO: verify
- Metric and definition/unit: > TODO: verify
- Baseline and final measurement: > TODO: verify
- Calculation: > TODO: verify
- Period, population, exclusions: > TODO: verify
- Evidence source and reproducibility: > TODO: verify
- Personal contribution / team attribution: > TODO: verify
- Limitations and caveats: > TODO: verify
- **How I measured this: (fill in)**

## Related notes

- [Resume deep-dive index](README.md)
- [Behavioral STAR method](../11-behavioral-hr/star-method.md)
- [Mistakes log](../99-revision/mistakes-log.md)

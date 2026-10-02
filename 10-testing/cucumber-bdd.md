---
title: "BDD with Cucumber"
tags: ["testing","bdd","cucumber"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# BDD with Cucumber

## Definition

**Behavior-Driven Development (BDD)** is a collaborative process where developers, testers, and business stakeholders define the behavior of a system using a shared, human-readable language. **Cucumber** is the most popular tool for implementing BDD.

## Core Concepts

### 1. Gherkin Language
Cucumber uses **Gherkin**, a structured language that uses a specific set of keywords to describe scenarios:

- **Feature**: Describes the high-level functionality (e.g., `Feature: User Authentication`).
- **Scenario**: A specific test case (e.g., `Scenario: Successful login with valid credentials`).
- **Given**: The initial context/precondition.
- **When**: The action taken by the user.
- **Then**: The expected outcome/verification.
- **And / But**: Used to add more steps.

### 2. Step Definitions
Step definitions are the "glue" code. They map the human-readable Gherkin steps to actual executable code (TypeScript, Java, etc.).

### 3. Scenario Outlines
Used to run the same scenario with multiple sets of data.
**Example**:
```gherkin
Scenario Outline: Login attempt
  Given the user is on the login page
  When the user enters "<username>" and "<password>"
  Then they should see "<message>"

  Examples:
    | username | password | message           |
    | user1    | pass123  | Welcome!          |
    | user2    | wrong    | Invalid Password  |
```

## Working Code Example: BDD Implementation

This example shows the mapping from a Gherkin feature file to a Playwright step definition in TypeScript.

**Feature File (`login.feature`)**:
```gherkin
Feature: User Login
  Scenario: Successful Login
    Given the user is on the login page
    When the user enters valid credentials
    Then the user should be redirected to the dashboard
```

**Step Definition (`login.steps.ts`)**:
```ts
import { Given, When, Then } from '@cucumber/cucumber';
import { expect } from '@playwright/test';

Given('the user is on the login page', async function () {
  await this.page.goto('/login');
});

When('the user enters valid credentials', async function () {
  await this.page.fill('#username', 'valid_user');
  await this.page.fill('#password', 'valid_pass');
  await this.page.click('#submit');
});

Then('the user should be redirected to the dashboard', async function () {
  await expect(this.page).toHaveURL('/dashboard');
});
```

**Complexity**:
- **Time**: The complexity is that of the underlying test (e.g., Playwright action).
- **Space**: $O(1)$ for the mapping; the memory usage is driven by the browser.

## Interview questions

### Q1: What is the primary goal of BDD?
**Model answer**: The goal is to bridge the communication gap between technical and non-technical stakeholders. By writing tests in plain English (Gherkin), we ensure that the developer's understanding of the feature matches the business analyst's intent *before* a single line of code is written.

### Q2: What is the difference between TDD and BDD?
**Model answer**: TDD (Test-Driven Development) is a developer-centric process focusing on the *implementation* (unit tests). BDD is a stakeholder-centric process focusing on the *behavior* and outcomes. In a healthy pipeline, BDD scenarios often drive the creation of the TDD unit tests.

### Q3: How do you handle data-driven testing in Cucumber?
**Model answer**: I use **Scenario Outlines** and **Examples tables**. This allows me to define a single logic flow and run it against a matrix of different inputs and expected outputs without duplicating the Gherkin steps.

### Q4: How do you avoid "Fragile Steps" in Cucumber?
**Model answer**: I avoid using UI-specific language in Gherkin. Instead of saying "When the user clicks the blue button," I say "When the user submits the form." This ensures that if the button color changes or the UI is redesigned, the business scenario remains valid and only the step definition needs to be updated.

### Q5: How do you integrate Cucumber into a CI/CD pipeline?
**Model answer**: I configure the Cucumber runner to output results in JSON or JUnit format. The CI tool (e.g., Jenkins) then parses these results to generate a test report and block the merge if any "Critical" scenario fails.

## Related notes

- [E2E Testing](../10-testing/playwright-selenium.md)
- [Testing Pyramid](../10-testing/test-pyramid.md)
- [TDD Workflow](../10-testing/tdd.md)

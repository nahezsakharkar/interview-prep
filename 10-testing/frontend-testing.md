---
title: "Frontend Testing Toolkit"
tags: ["testing","frontend","javascript"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Frontend Testing Toolkit

## 1. The Testing Pyramid for Frontend

To ensure a robust UI, use a mix of tests:
1. **Unit Tests**: Test a single function or a small component in isolation. (Fast, high volume).
2. **Integration Tests**: Test how multiple components work together. (Medium speed).
3. **E2E Tests**: Test the entire user flow in a real browser. (Slow, low volume).

## 2. Tooling Comparison

| Tool | Type | Best For | Key Feature |
| :--- | :--- | :--- | :--- |
| **Jest** | Unit/Integration | Logic, Hooks, Utils | Snapshot testing, Mocking |
| **React Testing Library**| Integration | User-centric UI behavior | Queries based on accessibility labels |
| **Playwright** | E2E | Complex flows, Cross-browser | Auto-waiting, Trace viewer, Headless |
| **Cypress** | E2E | Developer-centric testing | Real-time debugging, Time-travel |
| **Selenium** | E2E | Legacy, Enterprise | Wide language support |

## 3. Practical Implementation Examples

### Component Testing (Jest + RTL)
Focus on **behavior**, not implementation details.
```ts
import { render, screen, fireEvent } from '@testing-library/react';
import { LoginForm } from './LoginForm';

test('should show error on invalid login', async () => {
  render(<LoginForm />);
  
  fireEvent.change(screen.getByLabelText(/email/i), { target: { value: 'invalid' } });
  fireEvent.click(screen.getByRole('button', { name: /submit/i }));
  
  expect(await screen.findByText(/invalid email/i)).toBeInTheDocument();
});
```

### E2E Testing (Playwright)
Focus on the **critical path**.
```ts
import { test, expect } from '@playwright/test';

test('should complete checkout flow', async ({ page }) => {
  await page.goto('/cart');
  await page.click('text=Checkout');
  await page.fill('#address', '123 Main St');
  await page.click('#submit-payment');
  
  await expect(page.locator('.success-msg')).toBeVisible();
});
```

## 4. Advanced Testing Strategies

### Visual Regression Testing
Compare a screenshot of the current UI with a "baseline" image. If pixels differ by $> 1\%$, the test fails. Tools: **Percy, Applitools**.

### Flaky Test Mitigation
- **Avoid Hard-coded Sleeps**: Use `await waitFor()` or `findByText`.
- **Isolated State**: Reset the database or mock the API for every test case.
- **Retry Logic**: Configure CI to retry failed E2E tests once to filter out network glitches.

## 5. Interview Q&A

**Q: Why use React Testing Library instead of Enzyme?**
**A**: Enzyme focuses on internal state and implementation (e.g., `wrapper.state('open')`). RTL focuses on how the user interacts with the DOM (e.g., `screen.getByText('Open')`), making tests more resilient to refactoring.

**Q: When is an E2E test better than an Integration test?**
**A**: When you need to verify the "Last Mile" of the application: CDN caching, Authentication redirects, and actual Browser-to-Server network latency.

## Related notes

- [Test pyramid](10-testing/test-pyramid.md)
- [E2E testing](10-testing/e2e.md)

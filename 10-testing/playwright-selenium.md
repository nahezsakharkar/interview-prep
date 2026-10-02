---
title: "Modern E2E Testing: Playwright and Selenium"
tags: ["testing","e2e","automation"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Modern E2E Testing: Playwright and Selenium

## Definition

End-to-End (E2E) testing validates the entire software system from start to finish, including its integration with external interfaces. While Selenium was the industry standard for decades, Playwright is the modern choice for faster, more reliable testing.

## Selenium vs Playwright

| Feature | Selenium | Playwright |
| :--- | :--- | :--- |
| **Architecture** | HTTP-based (JSON Wire Protocol/W3C) | WebSocket-based (CDP) |
| **Speed** | Slower (due to HTTP overhead) | Extremely Fast |
| **Auto-waiting** | Manual (`implicitlyWait`, `WebDriverWait`) | Built-in (waits for actionability) |
| **Execution** | Single browser instance per driver | Browser Contexts (fast isolation) |
| **Network Control** | Limited | Native request/response interception |
| **Headless Mode** | Supported (configured) | Native and highly optimized |

## Playwright Core Concepts

### 1. Browser Contexts
Unlike Selenium, which requires a new browser process for each test, Playwright uses **Browser Contexts**. A context is like an incognito window: it has its own cookies and storage but shares the same browser process. This reduces test startup time from seconds to milliseconds.

### 2. Auto-waiting
Playwright eliminates "flaky tests" by automatically waiting for elements to be:
- Visible
- Stable (stopped animating)
- Enabled
- Editable

### 3. Network Interception
You can mock API responses to test edge cases (e.g., 500 errors) without needing a real backend.

## Working Code Example: Playwright E2E Test

This example demonstrates a modern E2E flow: logging in, intercepting a network request, and verifying a UI state.

```ts
import { test, expect } from '@playwright/test';

test('user can login and view dashboard', async ({ page }) => {
  // 1. Mock an API response to isolate the frontend
  await page.route('**/api/user/profile', async route => {
    await route.fulfill({
      status: 200,
      contentType: 'application/json',
      body: JSON.stringify({ name: 'Test User', role: 'Admin' }),
    });
  });

  // 2. Interaction
  await page.goto('/login');
  await page.fill('#username', 'test_user');
  await page.fill('#password', 'password123');
  await page.click('button[type="submit"]');

  // 3. Assertion (Auto-waits for the element to appear)
  const welcomeMsg = page.locator('.welcome-text');
  await expect(welcomeMsg).toBeVisible();
  await expect(welcomeMsg).toHaveText('Welcome, Test User');
});
```

**Complexity**:
- **Time**: $O(T)$ where $T$ is the total execution time of the browser actions.
- **Space**: $O(M)$ where $M$ is the memory used by the browser context.

## Interview questions

### Q1: Why is Playwright considered more stable than Selenium?
**Model answer**: Playwright uses a WebSocket connection to the browser, which allows it to listen to events in real-time. Its built-in "auto-waiting" mechanism means it only interacts with elements when they are actually ready, eliminating the need for fragile `sleep()` calls or complex custom wait logic.

### Q2: What is the benefit of using Browser Contexts?
**Model answer**: Contexts provide complete isolation for each test without the overhead of starting a new browser process. This allows us to run hundreds of tests in parallel on a single machine while ensuring that cookies, local storage, and cache from one test don't leak into another.

### Q3: How do you handle authentication in E2E tests to avoid logging in before every test?
**Model answer**: I use **Global Setup**. I log in once, save the authentication state (cookies and local storage) to a JSON file, and then load that state into every new Browser Context. This reduces the total test suite runtime by skipping the login flow for every single case.

### Q4: When would you still choose Selenium over Playwright?
**Model answer**: Selenium is the only choice if the project requires support for legacy browsers (like Internet Explorer) or very niche browser versions that Playwright's bundled binaries do not support.

### Q5: How do you test "flaky" UI elements that appear randomly?
**Model answer**: I use a combination of **Smart Retries** (configuring the test runner to retry a failed test 2-3 times) and **Network Throttling** (using Playwright to simulate slow 3G) to ensure the UI handles loading states correctly.

## Related notes

- [Testing Pyramid](../10-testing/test-pyramid.md)
- [TDD Workflow](../10-testing/tdd.md)
- [Frontend Security](../03-frontend/frontend-security.md)

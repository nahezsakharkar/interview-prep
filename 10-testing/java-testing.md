---
title: "Java Testing Frameworks (JUnit & Mockito)"
tags: ["testing","java","backend"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Java Testing Frameworks

## 1. JUnit 5 (The Standard)

JUnit 5 is the cornerstone of Java unit testing.

### Key Annotations
- `@Test`: Marks a method as a test.
- `@BeforeEach` / `@AfterEach`: Setup and teardown for every test.
- `@BeforeAll` / `@AfterAll`: Setup and teardown once per class (must be static).
- `@ParameterizedTest`: Runs the same test with different inputs.
- `@Disabled`: Skips a test.

### Assertions
- `assertEquals(expected, actual)`
- `assertTrue(condition)`
- `assertThrows(Exception.class, () -> { ... })`

## 2. Mockito (Isolating Dependencies)

Mockito allows you to create "fake" versions of dependencies to test logic in isolation.

### Core Concepts
- **`@Mock`**: Creates a mock object.
- **`@InjectMocks`**: Injects mocks into the object under test.
- **`when(...).thenReturn(...)`**: Defines the behavior of a mock.
- **`verify(...)`**: Ensures a method was called with specific arguments.

### Practical Example
```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    void testGetUser_Success() {
        User mockUser = new User("1", "John");
        when(userRepository.findById("1")).thenReturn(Optional.of(mockUser));

        User result = userService.getUserById("1");

        assertEquals("John", result.getName());
        verify(userRepository, times(1)).findById("1");
    }
}
```

## 3. BDD with Cucumber (Gherkin)

Behavior Driven Development (BDD) uses human-readable language to define tests.

### The Gherkin Syntax
Written in `.feature` files:
```gherkin
Feature: User Login
  Scenario: Successful login with valid credentials
    Given the user is on the login page
    When the user enters "user@example.com" and "password123"
    And clicks the login button
    Then they should be redirected to the dashboard
```

### Step Definitions
Each Gherkin line is mapped to a Java method:
```java
@Given("the user is on the login page")
public void navigateToLogin() {
    driver.get("https://app.example.com/login");
}
```

## 4. Testing Strategy Matrix

| Test Level | Tool | Focus | Speed |
| :--- | :--- | :--- | :--- |
| **Unit** | JUnit + Mockito | Single method / logic | Extremely Fast |
| **Integration**| SpringBootTest | DB / API boundaries | Medium |
| **Contract** | Pact | API Agreement | Medium |
| **Acceptance** | Cucumber / Selenium | User stories | Slow |

## Related notes

- [Test pyramid](10-testing/test-pyramid.md)
- [Integration testing](10-testing/integration-testing.md)

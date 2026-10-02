---
title: "Frontend Security"
tags: ["frontend","security","web-security"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Frontend Security

## Definition

Frontend security involves implementing defenses at the browser and application layer to protect users from malicious attacks and ensure the integrity of the data exchanged between the client and the server.

## Core Vulnerabilities and Mitigations

### 1. Cross-Site Scripting (XSS)
XSS occurs when an attacker injects malicious scripts into content delivered to other users.

- **Stored XSS**: Script is permanently stored on the server (e.g., in a database comment).
- **Reflected XSS**: Script is "reflected" off a web server via a URL parameter or form input.
- **DOM-based XSS**: The vulnerability exists in client-side code rather than server-side code.

**Mitigations**:
- **Escaping/Encoding**: Always encode user input before rendering it in HTML. React does this by default (`{userInput}`).
- **Avoid `dangerouslySetInnerHTML`**: Use it only when absolutely necessary and with a sanitizer like `DOMPurify`.
- **Content Security Policy (CSP)**: Use a `Content-Security-Policy` HTTP header to restrict which scripts can execute and where they can be loaded from.

### 2. Cross-Site Request Forgery (CSRF)
CSRF tricks a logged-in user into submitting a malicious request to a different website where they are authenticated.

**Mitigations**:
- **Anti-CSRF Tokens**: Include a unique, unpredictable token in every state-changing request. The server verifies the token before processing the request.
- **SameSite Cookie Attribute**: Set cookies to `SameSite=Lax` or `SameSite=Strict` to prevent the browser from sending cookies with cross-site requests.
- **Custom Headers**: Require a custom header (e.g., `X-Requested-With`) for API calls, as this forces the browser to perform a CORS pre-flight check.

### 3. Cross-Origin Resource Sharing (CORS)
CORS is a browser security mechanism that restricts how a script on one origin can interact with resources from another origin.

**How it works**:
1. The browser sends a "Pre-flight" request (`OPTIONS` method) to the server.
2. The server responds with headers like `Access-Control-Allow-Origin`.
3. The browser allows the request only if the origin matches the allowed list.

**Common Pitfalls**:
- **Wildcard Origin**: Setting `Access-Control-Allow-Origin: *` is dangerous for authenticated endpoints.
- **Credential Handling**: To send cookies/auth headers, the client must set `withCredentials: true` and the server must set `Access-Control-Allow-Credentials: true`.

## Secure Storage Comparison

| Storage | Accessible by JS? | Persists after Tab Close? | Sent with HTTP Request? | Security Risk |
| :--- | :--- | :--- | :--- | :--- |
| **localStorage** | Yes | Yes | No | High (XSS can steal data) |
| **sessionStorage** | Yes | No | No | Medium (XSS can steal data) |
| **Cookies (Standard)** | Yes | Optional | Yes | High (XSS + CSRF) |
| **Cookies (HttpOnly)** | **No** | Optional | **Yes** | Low (XSS cannot read; still CSRF risk) |

**Recommendation**: Store JWTs or Session IDs in **HttpOnly, Secure, SameSite=Lax** cookies to protect them from XSS.

## Working Code Example

This example demonstrates a simple implementation of a "Sanitization" wrapper to prevent XSS when you must render HTML.

```ts
import DOMPurify from 'dompurify';

interface SanitizeProps {
  htmlContent: string;
  children?: React.ReactNode;
}

const SafeHTML: React.FC<SanitizeProps> = ({ htmlContent }) => {
  // Sanitize the HTML string before passing it to dangerouslySetInnerHTML
  const cleanHTML = DOMPurify.sanitize(htmlContent, {
    ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'a'],
    ALLOWED_ATTR: ['href']
  });

  return (
    <div 
      dangerouslySetInnerHTML={{ __html: cleanHTML }} 
    />
  );
};

// Usage:
// <SafeHTML htmlContent="Hello <img src=x onerror=alert(1)> <b>User</b>" />
// Result: <div>Hello <b>User</b></div> (The malicious img tag is removed)
```

**Complexity**:
- **Time**: $O(N)$ where $N$ is the length of the HTML string.
- **Space**: $O(N)$ for the resulting sanitized string.

## Interview questions

### Q1: What is the difference between XSS and CSRF?
**Model answer**: XSS is about executing malicious scripts in the user's browser to steal data (like cookies). CSRF is about tricking the user's browser into performing an action on a different site using the user's existing session. XSS targets the *trust the user has in the site*, while CSRF targets the *trust the site has in the user's browser*.

### Q2: How does a CSP help prevent XSS?
**Model answer**: A Content Security Policy (CSP) is an HTTP header that tells the browser exactly which sources of content (scripts, styles, images) are trusted. If an attacker manages to inject a `<script>` tag pointing to a malicious domain, the browser will block the execution because that domain is not in the CSP allow-list.

### Q3: Why should you use `HttpOnly` cookies for authentication tokens?
**Model answer**: `HttpOnly` cookies cannot be accessed via JavaScript (`document.cookie`). This means that even if an attacker successfully executes an XSS attack, they cannot programmatically steal the session token to perform session hijacking.

### Q4: What is a "Pre-flight" request in CORS?
**Model answer**: A pre-flight request is an `OPTIONS` request sent by the browser before the actual request to check if the server permits the cross-origin call. This happens for "non-simple" requests (e.g., those using `PUT`, `DELETE`, or custom headers).

### Q5: How do you protect against CSRF if you aren't using cookies for auth?
**Model answer**: If you use a `Bearer` token in the `Authorization` header (stored in memory), the browser does not automatically attach it to cross-site requests. This inherently mitigates CSRF because the attacker cannot force the browser to send the token.

## Related notes

- [JWT and OAuth2](../04-backend/jwt-oauth2.md)
- [Browser internals](../03-frontend/browser-internals.md)
- [Next.js](../03-frontend/nextjs.md)

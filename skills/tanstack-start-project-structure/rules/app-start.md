---
title: Global Middleware Lives in src/start.ts
impact: MEDIUM
impactDescription: request-wide behavior is configured in one place
tags: app, createStart, middleware
---

## Global Middleware Lives in src/start.ts

**Impact: MEDIUM (request-wide behavior is configured in one place)**

`src/start.ts` exports the `createStart` instance with global request and server-function middleware (CSRF, logging, auth context). Features never register global middleware themselves.

```ts
export const startInstance = createStart(() => ({
  requestMiddleware: [csrfMiddleware],
}));
```

---
title: Split Configuration into Client and Server Modules
impact: MEDIUM
impactDescription: server secrets never reach the client bundle
tags: app, config, env
---

## Split Configuration into Client and Server Modules

**Impact: MEDIUM (server secrets never reach the client bundle)**

`config/client.ts` exposes values safe for the browser (`VITE_`-prefixed); `config/server.ts` exposes server-only values. Both validate their environment with a schema and are the only public config API. Shared helpers (`config/common.ts`) are internal: app code never imports them directly.

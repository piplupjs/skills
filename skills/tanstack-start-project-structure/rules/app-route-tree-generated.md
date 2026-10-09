---
title: Regenerate the Route Tree, Never Edit It
impact: MEDIUM
impactDescription: the route tree always matches the files
tags: app, routeTree, codegen
---

## Regenerate the Route Tree, Never Edit It

**Impact: MEDIUM (the route tree always matches the files)**

`routeTree.gen.ts` is generated from the route files (by the Vite plugin, or `tsr generate`). Keep it under `generated/` when the project has one (`generatedRouteTree` in the plugin options and `tsr.config.json`). Never edit it by hand; after adding, moving, or renaming a route file, regenerate it and commit the result.

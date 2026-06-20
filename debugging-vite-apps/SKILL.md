---
name: debugging-vite-apps
description: Use when a Vite/bundler-served web app shows a blank page, runtime crash, or module error — especially when tsc and build pass but the browser fails
---

# Debugging Vite Apps

## Overview

Vite ESM module resolution is stricter than TypeScript at runtime. A blank page with passing tsc/build almost always means a runtime JS error visible only in the browser console.

**Core principle:** Browser console is the single source of truth for blank-page bugs. Get it first, investigate second.

## When to Use

- Blank white page in browser, dev server running
- `tsc --noEmit` passes but app crashes at runtime
- `SyntaxError: does not provide an export named` errors
- Module resolution errors in Vite dev mode
- API calls failing silently (dotenv, model names, auth)

## Quick Reference

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Blank page, tsc passes | Type-only import used as value | Remove from value imports, use `import type` |
| `does not provide an export named 'X'` | X is a TypeScript type, not a runtime value | Check if X exists at runtime in the bundled module |
| React error boundary doesn't catch it | Module-level import error (before React mounts) | Error boundaries only catch render-phase errors |
| API returns "key not set" despite .env | `load_dotenv()` doesn't override existing env vars | Use `load_dotenv(override=True)` |
| API returns 404 on model name | Hallucinated model ID | Verify model IDs against official docs |
| Port conflict after restart | Stale process on port | `lsof -ti:PORT \| xargs kill` before restarting |

## The Vite ESM Trap

TypeScript type-only exports (like `DecorationSet` from `@codemirror/view`) pass `tsc --noEmit` when imported as values. But Vite's ESM loader checks actual JavaScript exports at runtime and crashes:

```
Uncaught SyntaxError: The requested module '...' does not provide an export named 'DecorationSet'
```

**Why tsc doesn't catch it:** TypeScript sees the type declaration and allows the import. It doesn't distinguish between type-only and value exports during type checking.

**Why vite build may still pass:** Tree-shaking can remove unused imports. The error only surfaces when the import is actually resolved at runtime.

**Fix pattern:**
```typescript
// BAD - crashes Vite if DecorationSet is type-only
import { EditorView, Decoration, DecorationSet } from '@codemirror/view'

// GOOD - separate type imports
import { EditorView, Decoration } from '@codemirror/view'
import type { DecorationSet } from '@codemirror/view'
```

## Debugging Order (Blank Page)

1. **Get browser console output** — ask the user or check DevTools. This is step 1, always.
2. **Read the error message** — Vite errors are specific and actionable.
3. **If import error:** check whether the named export exists as a runtime value (not just a type).
4. **If no console error:** check Network tab for failed resource loads.
5. **Do NOT:** add React error boundaries for module-level crashes, kill dev servers, or investigate server-side code.

## Common Mistakes

- **Investigating servers when the browser has the answer.** Blank page = JS error. The server is fine if it served the HTML.
- **Adding React error boundaries for import crashes.** Error boundaries catch render errors. Module-level import failures happen before React even loads.
- **Killing the dev server during debugging.** Creates a second problem (port conflicts, lost HMR state). Leave it running.
- **Trusting tsc as proof the code runs.** tsc checks types. Vite checks actual ESM exports. They disagree on type-only exports.
- **Using `load_dotenv()` without `override=True`.** If the env var exists (even as empty string), the .env value is silently ignored.

---
name: gstack-browse
description: |
  QA testing and site dogfooding via browser automation. Navigate URLs, interact with elements,
  verify page state, take screenshots, check responsive layouts, test forms, and assert element
  states. Use when you need to test a feature, verify a deployment, dogfood a user flow, or
  file a bug with evidence.
---

# browse: QA Testing & Dogfooding

Use the Claude Preview MCP tools (preview_snapshot, preview_screenshot, preview_click, preview_fill, preview_eval, preview_inspect, preview_network, preview_console_logs) or Claude in Chrome MCP tools when a dev server isn't running.

## Tool Selection

- **Claude Preview**: When a dev server is running (started via preview_start). Preferred for local development.
- **Claude in Chrome**: When testing deployed URLs or sites without a local server.

## Core QA Patterns

### 1. Verify a page loads correctly
```
preview_snapshot          → content loads?
preview_console_logs      → JS errors?
preview_network filter=failed → failed requests?
preview_inspect ".main-content" → key elements present?
```

### 2. Test a user flow
```
preview_snapshot          → see all interactive elements
preview_fill selector="#email" value="user@test.com"
preview_fill selector="#password" value="password"
preview_click selector="#submit"
preview_snapshot          → what changed after submit?
preview_inspect ".dashboard" → success state present?
```

### 3. Visual evidence for bug reports
```
preview_screenshot        → capture current state
preview_console_logs level=error → error log
preview_network filter=failed → failed requests
```

### 4. Assert element states
```
preview_inspect selector=".modal"        → visible?
preview_inspect selector="#submit-btn"   → check computed styles
preview_eval expression="document.querySelector('#agree-checkbox').checked"
preview_eval expression="document.activeElement.id"
```

### 5. Test responsive layouts
```
preview_resize preset=mobile
preview_screenshot
preview_resize preset=tablet
preview_screenshot
preview_resize preset=desktop
preview_screenshot
```

### 6. Inspect specific CSS properties
```
preview_inspect selector=".button" styles=["color", "background-color", "padding"]
```

### 7. Monitor network requests
```
preview_network                          → list all requests
preview_network filter=failed            → only failures
preview_network requestId="req-123"      → inspect response body
```

### 8. Check console output
```
preview_console_logs                     → all output
preview_console_logs level=error         → errors only
preview_console_logs level=warn          → warnings + errors
```

## Chrome MCP Equivalents

When using Claude in Chrome (for deployed sites without local server):

| Preview Tool | Chrome MCP Equivalent |
|---|---|
| preview_snapshot | read_page |
| preview_screenshot | computer action=screenshot |
| preview_click | computer action=left_click or find + click by ref |
| preview_fill | form_input |
| preview_eval | javascript_tool |
| preview_inspect | read_page + javascript_tool for computed styles |
| preview_network | read_network_requests |
| preview_console_logs | read_console_messages |
| preview_resize | resize_window |

## Workflow

1. **Navigate** to the target URL
2. **Snapshot** the page state (accessibility tree preferred over screenshot for structure)
3. **Interact** with elements using selectors or refs
4. **Verify** the result with snapshot/screenshot/inspect
5. **Document** findings with screenshots as evidence

## Important Rules

1. **Screenshot evidence for every finding.** No exceptions.
2. **Check console after every interaction.** JS errors that don't surface visually are still bugs.
3. **Test like a user.** Use realistic data. Walk through complete workflows end-to-end.
4. **Never include real credentials in reports.** Use `[REDACTED]`.
5. **Prefer accessibility snapshots over screenshots** for verifying content and structure. Use screenshots for visual/layout issues.
6. **Use preview_inspect for precise style verification** — more accurate than screenshots for colors, fonts, spacing.

---
name: gstack-qa
description: |
  Systematically QA test a web application. Use when asked to "qa", "QA", "test this site",
  "find bugs", "dogfood", or review quality. Three modes: full (systematic exploration),
  quick (30-second smoke test), regression (compare against baseline). Produces structured
  report with health score, screenshots, and repro steps.
---

# /qa: Systematic QA Testing

You are a QA engineer. Test web applications like a real user — click everything, fill every form, check every state. Produce a structured report with evidence.

Use Claude Preview MCP tools for local dev servers, Claude in Chrome MCP tools for deployed sites. See gstack-browse skill for tool mapping.

## Setup

**Parse the user's request for these parameters:**

| Parameter | Default | Override example |
|-----------|---------|-----------------|
| Target URL | (required) | `https://myapp.com`, `http://localhost:3000` |
| Mode | full | `--quick`, `--regression` |
| Output dir | `.qa-reports/` | `Output to /tmp/qa` |
| Scope | Full app | `Focus on the billing page` |
| Auth | None | `Sign in first` |

**Create output directories:**

```bash
mkdir -p ".qa-reports/screenshots"
```

## Modes

### Full (default)
Systematic exploration. Visit every reachable page. Document 5-10 well-evidenced issues. Produce health score. Takes 5-15 minutes depending on app size.

### Quick (`--quick`)
30-second smoke test. Visit homepage + top 5 navigation targets. Check: page loads? Console errors? Broken links? Produce health score. No detailed issue documentation.

### Regression (`--regression`)
Run full mode, then load `baseline.json` from a previous run. Diff: which issues are fixed? Which are new? What's the score delta? Append regression section to report.

## Workflow

### Phase 1: Initialize

1. Create output directories
2. Start the dev server if needed (preview_start) or navigate to deployed URL
3. Start timer for duration tracking

### Phase 2: Authenticate (if needed)

If the user specified auth:
1. Navigate to login page
2. Take a snapshot to find form fields
3. Fill credentials (NEVER include real passwords in report — use `[REDACTED]`)
4. Submit and verify login succeeded

If CAPTCHA blocks you: Tell the user to complete it manually.

### Phase 3: Orient

Get a map of the application:

1. Take an accessibility snapshot of the landing page
2. Take a screenshot for visual reference
3. Check console for errors on landing
4. Identify navigation structure and key pages

**Detect framework** (note in report metadata):
- `__next` in HTML or `_next/data` requests: Next.js
- `wp-content` in URLs: WordPress
- Astro-specific markers: Astro
- Client-side routing with no page reloads: SPA

### Phase 4: Explore

Visit pages systematically. At each page:

1. Take accessibility snapshot
2. Take screenshot
3. Check console for errors

Then follow the **per-page checklist:**

1. **Visual scan** — Look at screenshot for layout issues
2. **Interactive elements** — Click buttons, links, controls. Do they work?
3. **Forms** — Fill and submit. Test empty, invalid, edge cases
4. **Navigation** — Check all paths in and out
5. **States** — Empty state, loading, error, overflow
6. **Console** — Any new JS errors after interactions?
7. **Responsiveness** — Check mobile viewport:
   ```
   preview_resize preset=mobile
   preview_screenshot
   preview_resize preset=desktop
   ```

**Depth judgment:** Spend more time on core features (homepage, dashboard, checkout, search) and less on secondary pages (about, terms, privacy).

**Quick mode:** Only visit homepage + top 5 navigation targets. Skip the per-page checklist — just check: loads? Console errors? Broken links visible?

### Phase 5: Document

Document each issue **immediately when found** — don't batch them.

**Two evidence tiers:**

**Interactive bugs** (broken flows, dead buttons, form failures):
1. Screenshot before the action
2. Perform the action
3. Screenshot showing the result
4. Write repro steps referencing screenshots

**Static bugs** (typos, layout issues, missing images):
1. Single screenshot showing the problem
2. Describe what's wrong

**Write each issue to the report immediately.**

### Phase 6: Wrap Up

1. Compute health score using the rubric below
2. Write "Top 3 Things to Fix" — the 3 highest-severity issues
3. Write console health summary — aggregate all console errors across pages
4. Update severity counts in the summary table
5. Fill in report metadata — date, duration, pages visited, screenshot count, framework
6. Save baseline JSON for future regression runs

**Regression mode:** After writing the report, load the baseline file. Compare:
- Health score delta
- Issues fixed (in baseline but not current)
- New issues (in current but not baseline)
- Append the regression section to the report

## Health Score Rubric

Compute each category score (0-100), then take the weighted average.

### Console (weight: 15%)
- 0 errors: 100
- 1-3 errors: 70
- 4-10 errors: 40
- 10+ errors: 10

### Links (weight: 10%)
- 0 broken: 100
- Each broken link: -15 (minimum 0)

### Per-Category Deductions (Visual, Functional, UX, Content, Performance, Accessibility)
Each category starts at 100. Deduct per finding:
- Critical: -25
- High: -15
- Medium: -8
- Low: -3

Minimum 0 per category.

### Weights
| Category | Weight |
|----------|--------|
| Console | 15% |
| Links | 10% |
| Visual | 10% |
| Functional | 20% |
| UX | 15% |
| Performance | 10% |
| Content | 5% |
| Accessibility | 15% |

### Final Score
`score = sum(category_score * weight)`

## Framework-Specific Guidance

### Next.js
- Check for hydration errors in console
- Monitor `_next/data` requests — 404s indicate broken data fetching
- Test client-side navigation (click links, don't just navigate) — catches routing issues

### Astro
- Check that static pages load without JS errors
- Test any islands (interactive components) — do they hydrate correctly?
- Verify that non-JS pages work with JS disabled (if applicable)

### General SPA (React, Vue, Angular)
- Use accessibility snapshots for navigation — link extraction misses client-side routes
- Check for stale state (navigate away and back — does data refresh?)
- Test browser back/forward — does the app handle history correctly?

## Output Structure

```
.qa-reports/
├── qa-report-{domain}-{YYYY-MM-DD}.md    # Structured report
├── screenshots/
│   ├── initial.png
│   ├── issue-001-before.png
│   ├── issue-001-after.png
│   └── ...
└── baseline.json                          # For regression mode
```

## Report Template

```markdown
# QA Report: {domain}

**Date:** YYYY-MM-DD
**Duration:** Xm Ys
**Mode:** full | quick | regression
**Framework:** detected framework
**Pages visited:** N
**Screenshots:** N

## Health Score: XX/100

| Category | Score | Weight | Issues |
|----------|-------|--------|--------|
| Console | X | 15% | N |
| Links | X | 10% | N |
| Visual | X | 10% | N |
| Functional | X | 20% | N |
| UX | X | 15% | N |
| Performance | X | 10% | N |
| Content | X | 5% | N |
| Accessibility | X | 15% | N |

## Top 3 Things to Fix

1. ...
2. ...
3. ...

## Issues

### ISSUE-001: {title}
**Severity:** critical | high | medium | low
**Category:** console | links | visual | functional | ux | performance | content | accessibility
**Page:** {url}

**Steps to reproduce:**
1. ...

**Evidence:** screenshots/issue-001-before.png, screenshots/issue-001-after.png

---
```

## Important Rules

1. **Repro is everything.** Every issue needs at least one screenshot. No exceptions.
2. **Verify before documenting.** Retry once to confirm reproducibility.
3. **Never include credentials.** Write `[REDACTED]` for passwords.
4. **Write incrementally.** Append each issue as you find it. Don't batch.
5. **Never read source code.** Test as a user, not a developer.
6. **Check console after every interaction.** JS errors that don't surface visually are still bugs.
7. **Test like a user.** Use realistic data. Walk through complete workflows end-to-end.
8. **Depth over breadth.** 5-10 well-documented issues with evidence > 20 vague descriptions.

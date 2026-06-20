---
name: gstack-ship
description: |
  Ship workflow: merge main, run tests, review diff, commit, push, create PR.
  Use when asked to "ship", "ship it", or "create a PR for this work".
---

# Ship: Automated Ship Workflow

You are running the `/ship` workflow. This is a **non-interactive, fully automated** workflow. Do NOT ask for confirmation at any step. The user said `/ship` which means DO IT. Run straight through and output the PR URL at the end.

**Only stop for:**
- On `main`/`master` branch (abort)
- Merge conflicts that can't be auto-resolved (stop, show conflicts)
- Test failures (stop, show failures)
- Pre-landing review finds CRITICAL issues

**Never stop for:**
- Uncommitted changes (always include them)
- Commit message approval (auto-commit)
- Multi-file changesets (auto-split into bisectable commits)

---

## Step 1: Pre-flight

1. Check the current branch. If on `main` or `master`, **abort**: "You're on main. Ship from a feature branch."

2. Run `git status` (never use `-uall`). Uncommitted changes are always included — no need to ask.

3. Run `git diff main...HEAD --stat` and `git log main..HEAD --oneline` to understand what's being shipped.

4. **Detect project type** by checking for:
   - `package.json` → Node/JS project (check for test scripts)
   - `pyproject.toml` or `setup.py` → Python project
   - `*.csproj` or `*.sln` → .NET project
   - `Cargo.toml` → Rust project
   - `go.mod` → Go project
   - Multiple indicators → polyglot (run all applicable test suites)

---

## Step 2: Merge origin/main (BEFORE tests)

Fetch and merge `origin/main` into the feature branch so tests run against the merged state:

```bash
git fetch origin main && git merge origin/main --no-edit
```

**If there are merge conflicts:** Try to auto-resolve if they are simple. If conflicts are complex or ambiguous, **STOP** and show them.

**If already up to date:** Continue silently.

---

## Step 3: Run tests (on merged code)

Run the test suite(s) appropriate for the detected project type:

| Project Type | Test Command |
|---|---|
| Node (package.json has "test") | `npm test` |
| Node (Vitest/Jest detected) | `npx vitest run` or `npx jest` |
| Python (pytest) | `python -m pytest` |
| Python (unittest) | `python -m unittest discover` |
| .NET | `dotnet test` |
| Rust | `cargo test` |
| Go | `go test ./...` |
| Astro | `npm run build` (static sites — build IS the test) |

If multiple test suites exist, run them in parallel where possible.

**If no test command is found:** Run `npm run build` or equivalent build command. If nothing exists, note "No tests configured" and continue.

**If any test fails:** Show the failures and **STOP**. Do not proceed.

**If all pass:** Continue — just note the counts briefly.

---

## Step 4: Pre-Landing Review

Review the diff for structural issues that tests don't catch.

1. Run `git diff origin/main` to get the full diff.

2. Check for these categories:

**CRITICAL (must fix):**
- SQL injection or unsanitized user input
- Hardcoded secrets, API keys, or credentials
- Deleted or corrupted migration/schema files
- Breaking changes to public APIs without versioning

**INFORMATIONAL (note in PR):**
- Missing error handling on external calls
- TODO/FIXME/HACK comments introduced
- Large files (>500 lines) that could be split
- Missing type annotations in TypeScript
- Console.log/print statements left in

3. Output: `Pre-Landing Review: N issues (X critical, Y informational)`

4. **If CRITICAL issues found:** For each, show the problem with `file:line`, recommend a fix, and ask: Fix now? Acknowledge and ship? False positive?
   - If user chose to fix: apply fixes, commit them, then **STOP** — tell user to run `/ship` again.
   - If user acknowledged all: continue.

5. **If only informational issues:** Output them and continue. Include in PR body.

---

## Step 5: Stage and Commit (bisectable chunks)

**Goal:** Create small, logical commits that work well with `git bisect`.

1. Stage all changes: `git add -A`

2. Analyze the diff and group changes into logical commits. Each commit = one coherent change.

3. **Commit ordering** (earlier commits first):
   - Infrastructure (config, migrations, schema)
   - Core logic (models, services, utilities)
   - Interface (controllers, views, components, pages)
   - Tests for the above
   - Documentation and metadata

4. **Rules:**
   - A module and its test file go in the same commit
   - If the total diff is small (< 50 lines across < 4 files), a single commit is fine
   - Each commit must be independently valid — no broken imports

5. Commit messages: `<type>: <summary>` (type = feat/fix/chore/refactor/docs)
   - Final commit gets co-author trailer:
   ```
   Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
   ```

---

## Step 6: Push

```bash
git push -u origin <branch-name>
```

---

## Step 7: Create PR

Create a pull request. Prefer `gh pr create` if available, otherwise output instructions for manual PR creation.

**Check for gh CLI:**
```bash
which gh 2>/dev/null
```

**If gh is available:**
```bash
gh pr create --title "<type>: <summary>" --body "$(cat <<'EOF'
## Summary
<bullet points describing what changed and why>

## Pre-Landing Review
<findings from Step 4, or "No issues found.">

## Test Results
<test suite results — pass counts, or "No tests configured">

🤖 Generated with [Claude Code](https://claude.com/claude-code)
EOF
)"
```

**If gh is NOT available:**
Output the PR details (title, body, base branch, head branch) and tell the user:
"gh CLI is not installed. Push completed. Create the PR manually or install gh: `brew install gh && gh auth login`"

**Output the PR URL** (or the push confirmation if no gh).

---

## Important Rules

- **Never skip tests.** If tests fail, stop.
- **Never force push.** Use regular `git push` only.
- **Never ask for confirmation** except for CRITICAL review findings.
- **Date format:** `YYYY-MM-DD`
- **Split commits for bisectability** when the diff is large enough to warrant it.
- **The goal is: user says `/ship`, next thing they see is the review + PR URL.**

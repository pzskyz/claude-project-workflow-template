---
description: Verify only - run verification for current changes
---

# Verify Only - Verification Only

## Environment

Run verification for current changes only. DO NOT modify code unless user asks.

## Input

$ARGUMENTS

## Process

### Step 1: View changes

```bash
git status --short
git diff --name-only
git diff
```

### Step 2: Identify affected area

- [ ] Identify changed files
- [ ] Identify change type:
  - Docs/config only?
  - Bug fix?
  - Feature?
  - Cross-system?
- [ ] Evaluate risk level

### Step 3: Read commands from CLAUDE.md

From `CLAUDE.md` → `Project Commands`:
- Test command
- Build command
- Lint command
- Typecheck command
- E2E command

### Step 4: Select verification level

| Level | When | Checks |
|-------|------|--------|
| 0 | Docs/config only | Check formatting |
| 1 | Surgical fix | Targeted test + lint/typecheck |
| 2 | Feature change | Tests + build + lint/typecheck |
| 3 | Cross-system | Tests + build + E2E |

### Step 5: Run verification

**Level 0:**
- Review changed files for formatting

**Level 1:**
```bash
[TARGETED_TEST_COMMAND]  # from CLAUDE.md
[LINT_COMMAND]          # from CLAUDE.md
[TYPECHECK_COMMAND]     # from CLAUDE.md (if available)
```

**Level 2:**
```bash
[TEST_COMMAND]          # from CLAUDE.md
[BUILD_COMMAND]         # from CLAUDE.md
[LINT_COMMAND]          # from CLAUDE.md
```

**Level 3:**
```bash
[TEST_COMMAND]          # from CLAUDE.md
[BUILD_COMMAND]         # from CLAUDE.md
[E2E_COMMAND]           # from CLAUDE.md
```

### Step 6: Report results

## Output: Verification Report

```markdown
## Verification Report

### Changes Summary
- **Files**: [count]
- **Type**: [docs/config/bug/feature/refactor]
- **Scope**: [surgical/feature/cross-system]

### Verification Level
[0/1/2/3]

### Checks Run

| Check | Command | Status |
|-------|---------|--------|
| Tests | [from CLAUDE.md] | ✅ Pass / ❌ Fail |
| Build | [from CLAUDE.md] | ✅ Pass / ❌ Fail / N/A |
| Lint | [from CLAUDE.md] | ✅ Pass / ❌ Fail / N/A |
| E2E | [from CLAUDE.md] | ✅ Pass / ❌ Fail / N/A |

### Results
<!-- Paste test output, build output -->

### Issues Found
- [none / list of issues]

### Skipped Checks
- [any skipped and why]

### Recommendation
[Ready to merge / Needs fixes / Manual review required]
```

## Rules

- **Never execute literal placeholders** like `[TEST_COMMAND]`
- Always read commands from `CLAUDE.md` first
- If command is unknown, inspect project files or ask user
- DO NOT modify code during verification
- If issues found → report but don't fix

## When to skip checks

- No E2E command in CLAUDE.md → note and skip
- No build step → skip
- Changes are docs-only → skip tests
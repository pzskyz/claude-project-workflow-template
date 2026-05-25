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
# View status
git status --short

# View file list
git diff --name-only

# View diff details
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

### Step 3: Select verification level

| Level | When | Checks |
|-------|------|--------|
| 0 | Docs/config only | Check formatting |
| 1 | Surgical fix | Unit tests + lint |
| 2 | Feature change | Tests + build |
| 3 | Cross-system | Tests + build + E2E |

### Step 4: Run verification

**Level 0:**
```bash
# Check formatting
<!-- CUSTOMIZE: prettier, markdownlint, etc. -->
```

**Level 1:**
```bash
# Run tests
{{TEST_COMMAND}}

# Run lint
{{LINT_COMMAND}}
```

**Level 2:**
```bash
# Run tests
{{TEST_COMMAND}}

# Run build
{{BUILD_COMMAND}}

# Run lint
{{LINT_COMMAND}}
```

**Level 3:**
```bash
# Run tests
{{TEST_COMMAND}}

# Run build
{{BUILD_COMMAND}}

# Run E2E
{{E2E_COMMAND}}
```

### Step 5: Report results

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
| Tests | `{{TEST_COMMAND}}` | ✅ Pass / ❌ Fail |
| Build | `{{BUILD_COMMAND}}` | ✅ Pass / ❌ Fail / N/A |
| Lint | `{{LINT_COMMAND}}` | ✅ Pass / ❌ Fail / N/A |
| E2E | `{{E2E_COMMAND}}` | ✅ Pass / ❌ Fail / N/A |

### Results
<!-- Paste test output, build output -->

### Issues Found
- [none / list of issues]

### Skipped Checks
- [any skipped and why]

### Recommendation
[Ready to merge / Needs fixes / Manual review required]
```

## When to skip checks

- No E2E command → note and skip
- No build step → skip
- Changes are docs-only → skip tests

## Notes

- DO NOT modify code during verification
- If issues found → report but don't fix
- If tests fail → describe issue and suggest fix approach
- If scope unclear → ask user
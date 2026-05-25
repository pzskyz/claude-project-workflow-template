---
description: Verify only - run verification for current changes
---

# Verify Only

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

### Step 3: Select verification level

| Level | When | Checks |
|-------|------|--------|
| 0 | Docs/config only | Manual review |
| 1 | Surgical fix | Targeted tests + lint/typecheck |
| 2 | Feature change | Tests + build + lint/typecheck |
| 3 | Cross-system | Tests + build + E2E |

### Step 4: Run verification

Read commands from `CLAUDE.md` → `Project Commands`.

- Never execute literal placeholders like `{{TEST_COMMAND}}`
- Use commands from CLAUDE.md
- If command is unknown, inspect project files

### Step 5: Report results

## Output

```markdown
## Verification Report

### Changes Summary
- **Files**: [count]
- **Type**: [docs/config/bug/feature/refactor]
- **Scope**: [surgical/feature/cross-system]

### Verification Level
[0/1/2/3]

### Commands Run
- [command] — [pass/fail/skipped]

### Build / Quality Status
- Tests: [pass/fail/skipped]
- Build: [pass/fail/skipped]
- Lint: [pass/fail/skipped]
- E2E: [pass/fail/skipped]

### Issues Found
- [none / list of issues]

### Recommendation
[Ready to merge / Needs fixes / Manual review required]
```

## Rules

- DO NOT modify code during verification
- If issues found → report but don't fix
- If scope unclear → ask user
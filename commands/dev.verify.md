---
description: Run repository verification based on change scope
---

# Dev Verify

Run repository verification using the commands defined in `CLAUDE.md`.

## Rules

- Read `CLAUDE.md` first.
- Use `CLAUDE.md` → `Project Commands` as the source of truth.
- Do not run literal placeholders such as `{{TEST_COMMAND}}`.
- If a command is missing or marked `UNKNOWN`, inspect project files to infer it.
- If still unknown, report it as skipped and ask the user.

## Workflow

### Step 1: Inspect changes

```bash
git status --short
git diff --name-only
```

### Step 2: Classify verification level

| Level | When                          | Required checks                 |
| ----- | ----------------------------- | ------------------------------- |
| 0     | Docs/config only              | Manual review or format check   |
| 1     | Surgical code change          | Targeted tests + lint/typecheck |
| 2     | Feature/behavior change       | Tests + build + lint/typecheck  |
| 3     | Cross-system/user-facing flow | Tests + build + E2E             |

### Step 3: Run checks

Use commands from `CLAUDE.md` → `Project Commands`.

**Level 0:**
- Run format check if available
- Otherwise manually review changed docs/config

**Level 1:**
- Run targeted test if available
- Run lint/typecheck if available

**Level 2:**
- Run test
- Run build
- Run lint/typecheck if available

**Level 3:**
- Run test
- Run build
- Run E2E
- Inspect E2E report if failures occur

## Auto-detect scope

### Heuristics for level selection

- **Level 0**: Only .md, .json (config), comments changed
- **Level 1**: < 3 files changed, no API/routing impact
- **Level 2**: Multiple files, or affects behavior/API
- **Level 3**: Cross-cutting concerns, auth, database, user flows

### Logic for detection

```bash
# Check what files changed
CHANGED_FILES=$(git diff --name-only)

# Check if only docs/config
if echo "$CHANGED_FILES" | grep -qvE '\.(ts|tsx|js|jsx|py|go)$'; then
  echo "Level 0"
fi

# Check if affecting critical paths
if echo "$CHANGED_FILES" | grep -qE "(auth|route|api|db)"; then
  echo "Level 3"
fi
```

## Finding Commands

If `CLAUDE.md` does not have the required command:

1. Inspect project files:
   - `package.json` (scripts section)
   - `pyproject.toml` (test configuration)
   - `Makefile` (targets)
   - `README.md` (setup instructions)
   - `.github/workflows/*.yml` (CI commands)

2. For monorepos, identify affected packages:
   ```bash
   PACKAGE=$(echo $CHANGED_FILES | grep -oE "packages/[^/]+" | head -1)
   ```

3. If command is still unknown, mark it as `UNKNOWN` and ask the user.

## When to skip checks

- Docs-only change → skip tests, only check formatting
- Config change with risk → ask user first
- Tests already run (CI) → note and skip
- Urgent hotfix → note and proceed

## Verification Report

```markdown
## Verification Report

### Level
[0/1/2/3]

### What Changed
[summary]

### Files Changed
- [file]

### Commands Run
- [command] — [pass/fail/skipped]

### Build / Quality Status
- Tests: [pass/fail/skipped]
- Build: [pass/fail/skipped]
- Lint: [pass/fail/skipped]
- Typecheck: [pass/fail/skipped]
- E2E: [pass/fail/skipped]

### Risks / Skipped Checks
- [reason]

### Recommendation
[Ready to merge | Needs fixes | Blocked]
```
---
description: Run verification - test, build, lint based on change scope
---

# Dev Verify

Run the verification pipeline appropriate for the scope and risk of the current changes.

<!-- IMPORTANT: Replace {{PLACEHOLDERS}} with actual project commands. -->
<!-- If a placeholder is not replaced, do not execute it. Inspect project files to find the correct command. If no command can be found, mark it as UNKNOWN and ask the user. -->

## Principles

- Verification level must match change scope
- Don't run too many or too few checks
- Report results clearly

## Process

### Step 1: Identify changes

```bash
git status --short
git diff --name-only
```

### Step 2: Determine verification level

| Level | When | Required Checks |
|-------|------|-----------------|
| 0 | Docs/config only | Check formatting |
| 1 | Single bug fix, small function | Unit tests + lint |
| 2 | Feature, behavior change | Tests + build |
| 3 | Cross-system, user-facing | Tests + build + E2E |

### Step 3: Run checks by level

#### Level 0: Docs/Config only

```bash
# Check formatting
<!-- CUSTOMIZE: Replace with appropriate command -->
<!-- Examples: npx prettier --check . -->
<!-- Examples: markdownlint *.md -->
```

#### Level 1: Surgical code change

```bash
<!-- CUSTOMIZE: Replace with project commands -->

# Run targeted tests
{{TEST_COMMAND}}

# Run linting
{{LINT_COMMAND}}

# Run typecheck if available
{{TYPECHECK_COMMAND}}
```

#### Level 2: Feature/behavior change

```bash
<!-- CUSTOMIZE: Replace with project commands -->

# Run tests
{{TEST_COMMAND}}

# Run build
{{BUILD_COMMAND}}

# Run linting
{{LINT_COMMAND}}
```

#### Level 3: Cross-system flow

```bash
<!-- CUSTOMIZE: Replace with project commands -->

# Run all tests
{{TEST_COMMAND}}

# Run build
{{BUILD_COMMAND}}

# Run E2E
{{E2E_COMMAND}}
```

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

## Output: Verification Report

```markdown
## Verification Report

- **Level**: [0/1/2/3]
- **What changed**: [description]
- **Files changed**: [list]
- **Tests run**: [commands]
- **Build status**: [pass/fail]
- **Lint status**: [pass/fail]
- **E2E status**: [pass/fail or N/A]
- **Risks/skipped**: [any concerns]
- **Recommendation**: [ready/needs-fixes]
```

## Examples for common stacks

### Next.js

```bash
npm run lint
npm run typecheck
npm test
npm run build
npx playwright test  # for E2E
```

### Python/FastAPI

```bash
pytest
ruff check .
mypy .
pytest tests/e2e/ -v
```

### Go

```bash
go test ./...
go build ./...
golangci-lint run
```

### Monorepo

```bash
# Detect affected packages
PACKAGE=$(echo $CHANGED_FILES | grep -oE "packages/[^/]+" | head -1)

# Run tests for affected package
pnpm --filter $PACKAGE test
pnpm --filter $PACKAGE build
```

## When to skip checks

- Docs-only change → skip tests, only check formatting
- Config change with risk → ask user first
- Tests already run (CI) → note and skip
- Urgent hotfix → note and proceed

## Customization markers

<!-- CUSTOMIZE: Update commands below for your project -->

Placeholders to replace:
- `{{TEST_COMMAND}}` - Test runner command
- `{{BUILD_COMMAND}}` - Build command
- `{{LINT_COMMAND}}` - Lint command
- `{{TYPECHECK_COMMAND}}` - Typecheck command (optional)
- `{{E2E_COMMAND}}` - E2E command (optional)
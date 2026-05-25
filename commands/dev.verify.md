---
description: Run verification - test, build, lint based on change scope
---

# Dev Verify

Run the verification pipeline appropriate for the scope and risk of the current changes.

## Principles

- Verification level must match change scope
- Don't run too many or too few checks
- Report results clearly
- Use commands from `CLAUDE.md` → `Project Commands` section

## Process

### Step 1: Read project commands

From `CLAUDE.md`, extract the `Project Commands` section:
- Test command
- Build command
- Lint command
- Typecheck command
- E2E command

### Step 2: Identify changes

```bash
git status --short
git diff --name-only
```

### Step 3: Determine verification level

| Level | When | Required Checks |
|-------|------|-----------------|
| 0 | Docs/config only | Check formatting |
| 1 | Single bug fix, small function | Targeted test + lint/typecheck |
| 2 | Feature, behavior change | Tests + build + lint/typecheck |
| 3 | Cross-system, user-facing | Tests + build + E2E |

### Step 4: Run checks by level

#### Level 0: Docs/Config only

- Review changed files for formatting
- No command execution required

#### Level 1: Surgical code change

```bash
# Run targeted tests (use targeted test command from CLAUDE.md)
{{TARGETED_TEST_COMMAND}}

# Run linting
{{LINT_COMMAND}}

# Run typecheck if available
{{TYPECHECK_COMMAND}}
```

#### Level 2: Feature/behavior change

```bash
# Run tests
{{TEST_COMMAND}}

# Run build
{{BUILD_COMMAND}}

# Run linting
{{LINT_COMMAND}}
```

#### Level 3: Cross-system flow

```bash
# Run tests
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

## Rules

- **Never execute literal placeholders** like `{{TEST_COMMAND}}`
- Always read commands from `CLAUDE.md` first
- If required command is missing, ask the user
- Prefer explicit commands over heuristics
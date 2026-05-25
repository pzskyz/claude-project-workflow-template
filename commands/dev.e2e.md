---
description: Run E2E tests or manual user flow verification
---

# Dev E2E

Run E2E tests using the E2E command defined in `CLAUDE.md`.

## Rules

- Read `CLAUDE.md` → `Project Commands` first.
- Use the project-defined E2E command.
- If E2E command is `UNKNOWN`, inspect project files for Playwright, Cypress, pytest e2e, or other E2E setup.
- If no E2E framework exists, perform API/manual user-flow verification and report that E2E is unavailable.

## When to Use

- **Level 3 verification**: Cross-system, user-facing changes
- **Critical paths**: Login, checkout, payment, auth flows
- **Before release**: Important feature needs full flow test
- **Regression**: Ensure changes don't break existing flows

## Workflow

1. Identify the user-facing flow affected by the change.
2. Read the E2E command from `CLAUDE.md`.
3. Discover available E2E tests before running specific files.
4. Run the smallest relevant E2E suite.
5. If tests fail, inspect logs, screenshots, traces, or reports.
6. Produce E2E report.

## Finding E2E Command

If `CLAUDE.md` → `Project Commands` has E2E marked as `UNKNOWN`:

1. Check for E2E frameworks:
   - Playwright: `playwright.config.ts`, `playwright.config.js`
   - Cypress: `cypress.config.ts`, `cypress.config.js`
   - Jest: `tests/e2e/`, `__e2e__/`
   - pytest: `tests/e2e/`, `e2e/`

2. Look in package.json scripts:
   ```bash
   grep -E "e2e|playwright|cypress" package.json
   ```

3. Check README for E2E instructions.

## Manual Verification

If no E2E framework exists, verify critical paths manually:

### Auth Flow
- [ ] Login with valid credentials → success
- [ ] Login with invalid credentials → error message
- [ ] Logout → session cleared
- [ ] Token expiration → redirect to login

### API Flow
```bash
# Test endpoints with curl
curl -X POST /api/login -d '{"email":"test@test.com"}'
curl /api/users/1
curl /api/users/999  # expect 404
```

### UI Flow (if applicable)
- [ ] Navigation between pages
- [ ] Form submission
- [ ] Loading states
- [ ] Error states

## E2E Report

```markdown
## E2E Verification Report

- **Scope**: [description of flow tested]
- **Framework**: [Playwright/Cypress/manual/None]
- **Tests run**: [count]
- **Passed**: [count]
- **Failed**: [count]

### Results
<!-- Test output or curl results -->

### Issues Found
- [list any failures]

### Recommendation
[ready / needs fixes / manual intervention required]
```

## When E2E is Unavailable

Report clearly:
- No E2E framework detected
- Which files were checked
- Suggest adding E2E tests if Level 3 verification is needed
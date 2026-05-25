---
description: Run E2E tests or manual user flow verification
---

# Dev E2E

Run end-to-end tests or verify manual user flows.

## When to use

- **Level 3 verification**: Cross-system, user-facing changes
- **Critical paths**: Login, checkout, payment, auth flows
- **Before release**: Important feature needs full flow test
- **Regression**: Ensure changes don't break existing flows

## Process

### Step 1: Read E2E command from CLAUDE.md

From `CLAUDE.md` → `Project Commands` → E2E section:
```bash
{{E2E_COMMAND}}
```

If not defined, inspect project files:
- `package.json` (scripts with "e2e", "test:e2e")
- `playwright.config.ts`, `cypress.config.ts`
- `README.md` (e2e instructions)

### Step 2: Run E2E tests

```bash
# Run all E2E tests
{{E2E_COMMAND}}

# Run specific test file (if applicable)
# {{E2E_COMMAND}} --spec path/to/test.spec.ts
```

### Step 3: View E2E report (if available)

```bash
# Show E2E report if command exists
{{E2E_REPORT_COMMAND}}
```

## Common E2E Frameworks

### Playwright
```bash
npx playwright test
npx playwright test --ui           # With UI
npx playwright test --headed       # See browser
npx playwright test --trace on    # With trace
```

### Cypress
```bash
npm run cypress:run
npm run cypress:open              # Open UI
```

### Jest + Supertest (API)
```bash
npm run test:e2e
npx jest tests/e2e
```

### pytest (Python)
```bash
pytest tests/e2e/ -v
```

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

## Output: E2E Report

```markdown
## E2E Verification Report

- **Scope**: [description of flow tested]
- **Framework**: [Playwright/Cypress/manual]
- **Tests run**: [count]
- **Passed**: [count]
- **Failed**: [count]
- **Duration**: [time]

### Results
<!-- Test output or curl results -->

### Issues Found
- [list any failures]

### Recommendation
- [ready / needs fixes / manual intervention required]
```

## Rules

- **Never execute literal placeholders** like `{{E2E_COMMAND}}`
- Always read from `CLAUDE.md` first
- If E2E command is unknown, inspect project files
- If still unknown, mark as `UNKNOWN` and ask user
- Note if no E2E framework exists (skip gracefully)

## When to skip E2E

- No E2E framework → note and skip
- Backend-only change that doesn't affect user flows → skip
- Time constraints → note and skip with reason
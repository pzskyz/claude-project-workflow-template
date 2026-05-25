---
description: Run E2E tests or manual user flow verification
---

# Dev E2E

Run end-to-end tests or verify manual user flows.

<!-- IMPORTANT: Replace {{PLACEHOLDERS}} with actual project commands. -->
<!-- If a placeholder is not replaced, do not execute it. Inspect project files to find the correct command. If no command can be found, mark it as UNKNOWN and ask the user. -->

## When to use

- **Level 3 verification**: Cross-system, user-facing changes
- **Critical paths**: Login, checkout, payment, auth flows
- **Before release**: Important feature needs full flow test
- **Regression**: Ensure changes don't break existing flows

## Process

### Step 1: Identify E2E command

```bash
<!-- CUSTOMIZE: Replace with project E2E command -->
{{E2E_COMMAND}}

# Or run specific test file
<!-- Example: npx playwright test tests/checkout.spec.ts -->
```

### Step 2: Or verify manually

If no E2E framework exists, verify manually:

1. **Identify flow to test**
2. **Check related endpoints**
3. **Test with curl/httpie**
4. **Verify response format**

### Step 3: Check critical paths

```bash
# Check auth flow
curl -X POST /api/login -d '{"email":"test@test.com"}'
# Expected: 200 + token

# Check data flow
curl /api/users/1
# Expected: user object

# Check error handling
curl /api/users/999
# Expected: 404 + error message
```

## Common E2E frameworks

### Playwright

```bash
# Run all tests
npx playwright test

# Run specific test
npx playwright test tests/checkout.spec.ts

# Run with UI
npx playwright test --ui

# Run headed (see browser)
npx playwright test --headed

# Run with trace
npx playwright test --trace on
```

### Cypress

```bash
# Run all tests
npm run cypress:run

# Run specific test
npx cypress run --spec "cypress/e2e/checkout.cy.js"

# Open Cypress UI
npm run cypress:open
```

### Jest + Supertest (API)

```bash
# Run E2E tests
npm run test:e2e
# or
npx jest tests/e2e
```

### pytest (Python)

```bash
# Run E2E tests
pytest tests/e2e/ -v
```

## Manual verification checklist

### Auth Flow
- [ ] Login with valid credentials → success
- [ ] Login with invalid credentials → error message
- [ ] Logout → session cleared
- [ ] Token expiration → redirect to login

### API Flow
- [ ] GET request → correct data
- [ ] POST request → data created
- [ ] PUT/PATCH → data updated
- [ ] DELETE → data removed
- [ ] Invalid input → proper error

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

## When to skip E2E

- No E2E framework → note and skip
- Backend-only change doesn't affect user flows → skip
- Time constraints → note and skip with reason

## Customization markers

<!-- CUSTOMIZE: Update E2E command for project -->

Placeholders to replace:
- `{{E2E_COMMAND}}` - E2E test runner command
  - Example: `npx playwright test`
  - Example: `npm run cypress:run`
  - Example: `pytest tests/e2e -v`
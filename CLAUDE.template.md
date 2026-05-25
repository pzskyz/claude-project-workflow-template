# {{PROJECT_NAME}}

<!-- Brief description of the project -->

## Project Overview

<!-- TODO: Fill in project purpose, target users, key problems solved -->

## Tech Stack

- **Framework**: {{FRAMEWORK}} ({{VERSION}})
- **Language**: {{LANGUAGE}} ({{VERSION}})
- **State Management**: {{STATE_MGMT}}
- **Architecture**: {{ARCHITECTURE_PATTERN}}
- **Database**: {{DATABASE}} ({{VERSION}})
- **Other Key Libraries**: {{KEY_LIBS}}

## Project Commands

This section is the **source of truth** for all project-specific commands.

If a command is not available, write `UNKNOWN` and explain why. Do not invent commands.

| Purpose       | Command                     | Notes                             |
| ------------- | --------------------------- | --------------------------------- |
| Setup         | `{{SETUP_COMMAND}}`         | Install dependencies              |
| Dev server    | `{{DEV_COMMAND}}`           | Start local development server    |
| Test          | `{{TEST_COMMAND}}`          | Run normal test suite             |
| Targeted test | `{{TARGETED_TEST_COMMAND}}` | Run one test file or pattern      |
| Build         | `{{BUILD_COMMAND}}`         | Production build or compile check |
| Lint          | `{{LINT_COMMAND}}`          | Static linting                    |
| Typecheck     | `{{TYPECHECK_COMMAND}}`     | Type checking, if applicable      |
| Format check  | `{{FORMAT_CHECK_COMMAND}}`  | Formatting check, if applicable   |
| E2E           | `{{E2E_COMMAND}}`           | End-to-end tests, if available    |
| E2E report    | `{{E2E_REPORT_COMMAND}}`    | Show E2E report, if available     |

## Command Resolution Rules

When executing slash commands:

1. Read `CLAUDE.md` first.
2. Use commands from `Project Commands`.
3. Never execute literal placeholders like `{{TEST_COMMAND}}`.
4. If a command is `UNKNOWN`, inspect project files:
   - `package.json`
   - `pyproject.toml`
   - `Makefile`
   - `README.md`
   - CI config (`.github/workflows/*.yml`)
   - Docker config
5. If still unknown, ask the user before running that check.

## Team Review Protocol

Use team review based on risk assessment.

### Full team review required for high-risk tasks

Spawn: architect, ux_designer, devil_advocate, tester

Required for:
- Architecture changes
- Auth/security
- Database schema/migrations
- Public API changes
- Cross-system flows
- Multi-tenant isolation
- Payment/billing
- User-facing critical flows
- Large refactors

### Lightweight review for low-risk tasks

Write for low-risk tasks:
- Assumptions
- Impacted files
- Test plan
- Risk level
- Verification commands

## Mandatory Verification Pipeline

Every source-code change must end with a verification report.

### Verification Levels

| Level | Use Case                | Required Checks                 |
| ----- | ----------------------- | ------------------------------- |
| 0     | Docs/config only        | Manual review or format check   |
| 1     | Surgical code change    | Targeted tests + lint/typecheck |
| 2     | Feature/behavior change | Tests + build + lint/typecheck  |
| 3     | Cross-system/user flow  | Tests + build + E2E             |

### Final Verification Report Format

```markdown
## Verification Report

- **What changed**: [description]
- **Files changed**: [list]
- **Tests run**: [commands executed]
- **Build status**: [pass/fail]
- **Lint/Typecheck status**: [pass/fail]
- **E2E status**: [pass/fail or N/A]
- **Risks/skipped checks**: [any concerns]
- **Recommendation**: [ready to merge / needs fixes]
```

## Coding Rules

### 1. Think Before Coding
- State assumptions explicitly
- Present multiple interpretations if ambiguous
- Ask questions early

### 2. Simplicity First
- No speculative features
- No premature abstractions
- 200 lines that could be 50? Rewrite.

### 3. Surgical Changes
- Touch only what you must
- Don't "improve" adjacent code
- Match existing style

### 4. Goal-Driven Execution
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
```

### 5. Durable & Organized Code
- No disposable scripts
- Reusable functions and modules
- Strategic code placement

### 6. Match Existing Patterns
- Follow the code style already in use
- Use existing utility functions
- Don't introduce conflicting conventions

## Error Handling

- Never silently swallow errors
- Log errors with context
- Handle edge cases explicitly

## Testing Guidelines

- Test behavior, not implementation
- Mock external dependencies
- Keep tests fast and isolated

## Notes

<!-- TODO: Add project-specific notes, conventions, or gotchas -->
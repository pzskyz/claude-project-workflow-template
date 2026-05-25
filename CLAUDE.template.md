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

## Standard Commands

### Setup

```bash
{{INSTALL_COMMAND}}
```

### Run Development

```bash
{{START_COMMAND}}
```

### Test

```bash
{{TEST_COMMAND}}
```

### Build

```bash
{{BUILD_COMMAND}}
```

### Lint / Typecheck

```bash
{{LINT_COMMAND}}
```

### E2E Tests

```bash
{{E2E_COMMAND}}
```

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

| Level | Use Case                | Required Checks                                                    |
| ----- | ----------------------- | ------------------------------------------------------------------ |
| 0     | Docs/config only        | Check formatting manually, no tests required                       |
| 1     | Surgical code change    | Run targeted unit tests, run lint/typecheck                        |
| 2     | Feature/behavior change | Add/update tests, run relevant unit/integration tests, run build   |
| 3     | Cross-system/user flow  | Unit/integration tests, build verification, E2E tests, update docs |

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
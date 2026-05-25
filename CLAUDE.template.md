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
| E2E report    | `{{E2E_REPORT_COMMAND}}`     | Show E2E report, if available     |

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

## Core Engineering Rules

These rules reduce common LLM coding mistakes. They bias toward caution over speed. For trivial tasks, use judgment.

### Think Before Coding

Do not assume. Do not hide confusion. Surface tradeoffs.

Before implementing:

- State assumptions explicitly.
- If multiple interpretations exist, present them instead of silently choosing one.
- If a simpler approach exists, say so.
- Push back when the requested solution seems overcomplicated or risky.
- If something is unclear, stop, name the confusion, and ask.

### Simplicity First

Implement the minimum code that solves the problem.

- Do not add features beyond what was asked.
- Do not introduce abstractions for single-use code.
- Do not add flexibility or configurability that was not requested.
- Avoid speculative error handling for impossible scenarios.
- If a solution is much longer than necessary, simplify it.

### Surgical Changes

Touch only what is required.

- Do not improve adjacent code, comments, or formatting.
- Do not refactor unrelated code.
- Match existing style, even if you would normally do it differently.
- If you notice unrelated dead code, mention it instead of deleting it.
- Remove only imports, variables, or functions made unused by your own changes.

Every changed line must trace directly to the user's request.

### Goal-Driven Execution

Define success criteria and loop until verified.

- "Add validation" → write tests for invalid inputs, then make them pass.
- "Fix a bug" → write or identify a failing test that reproduces it, then make it pass.
- "Refactor X" → ensure behavior is covered before and after.

For multi-step tasks, state a brief plan:

```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
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
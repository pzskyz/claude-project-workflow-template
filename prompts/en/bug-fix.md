---
description: Fix bug - standard workflow
---

# Fix Bug

## Environment

You are helping the user fix a bug. Approach systematically.

## Input

$ARGUMENTS

## Process

### Phase 1: Reproduce bug

- [ ] Confirm bug:
  - **Actual behavior**: [paste description]
  - **Expected behavior**: [paste expected]
- [ ] Reproduce if possible
- [ ] Collect logs, error messages, screenshots if any

### Phase 2: Trace flow

- [ ] Read `CLAUDE.md` for project context
- [ ] Find entry point of buggy flow
- [ ] Trace through files
- [ ] Identify root cause hypothesis

### Phase 3: Analyze

- [ ] Create `.claude-analysis.md`:
  ```markdown
  ## Bug Analysis

  ### Problem
  [Short description]

  ### Current Flow
  1. [Step 1]
  2. [Step 2]
  ...

  ### Root Cause Hypothesis
  [Hypothesis 1]
  [Hypothesis 2]

  ### Evidence
  - [Log line 1]
  - [Error message]

  ### Test Plan
  - Unit test: [description]
  - Manual test: [steps]

  ### Impacted Files
  - [file 1]
  - [file 2]

  ### Risk Level
  [Low/Medium/High]

  ### Verification Level
  [1/2/3]
  ```

- [ ] Confirm root cause with user

### Phase 4: Implement fix

- [ ] Read related files
- [ ] Apply fix:
  - Surgical changes only
  - No extensive refactoring
  - Match existing patterns
- [ ] Write/update tests to cover bug

### Phase 5: Verify

- [ ] Reproduce bug → confirm fixed
- [ ] Run tests (from `CLAUDE.md` → `Project Commands`)
- [ ] Run lint/build if needed

### Phase 6: Finalize

- [ ] Review diff
- [ ] Ensure only necessary changes
- [ ] Generate verification report

## Final Output

```markdown
## Bug Fix Verification Report

### Bug
[Short title]

### Root Cause
[Root cause description]

### Fix Applied
[Fix description]

### Files Changed
- [file 1]
- [file 2]

### Tests
- New test: [description]
- All tests passing: [yes/no]

### Verification
| Check | Status |
|-------|--------|
| Bug reproduced | ✅ |
| Bug fixed | ✅ |
| Tests pass | ✅ |
| Build pass | ✅ |

### Recommendation
[Ready to merge]
```

## Notes

- Prioritize reproducing bug before fixing
- If cannot reproduce → ask user for more context
- Fix must cover edge cases, not just happy path
- After fix → confirm bug is gone
- Use commands from `CLAUDE.md` → `Project Commands` section
---
description: Refactor code - preserve behavior
---

# Refactor

## Environment

You are helping the user refactor code. Goal: improve structure WITHOUT changing behavior.

## Input

$ARGUMENTS

## Process

### Phase 1: Define scope

- [ ] Identify refactor target:
  - Function/module to refactor?
  - Problem to solve?
- [ ] Ask user:
  - Why refactor? (performance, readability, maintainability?)
  - Any deadlines/constraints?
- [ ] Define boundaries: what NOT to refactor

### Phase 2: Understand current behavior

- [ ] Read `CLAUDE.md` for project context
- [ ] Trace current flow
- [ ] Identify public API contract to preserve:
  - Function signatures
  - Return values
  - Side effects
  - Error handling behavior

### Phase 3: Analyze

- [ ] Create `.claude-analysis.md`:
  ```markdown
  ## Refactor Analysis

  ### Target
  [File/function/module to refactor]

  ### Current State
  - LOC: [line count]
  - Complexity: [description]
  - Issues: [list of problems]

  ### Behavior to Preserve
  - [API 1]
  - [API 2]
  - [Edge cases]

  ### Proposed Changes
  [Describe approach]

  ### Regression Test Plan
  - Test 1: [description]
  - Test 2: [description]

  ### Risk Level
  [Low/Medium/High]

  ### Verification Level
  [1/2/3]
  ```

- [ ] Confirm approach with user

### Phase 4: Implement

- [ ] Read current code
- [ ] Implement refactor:
  - Change internals
  - KEEP public API intact
  - KEEP behavior intact
- [ ] Update internal tests if needed

### Phase 5: Verify

- [ ] Run all tests from `CLAUDE.md` → `Project Commands`
- [ ] Verify behavior unchanged
- [ ] Run lint/build

### Phase 6: Finalize

- [ ] Review diff
- [ ] Ensure:
  - Public API unchanged
  - Tests still pass
  - No breaking changes
- [ ] Generate verification report

## Final Output

```markdown
## Refactor Verification Report

### Target
[File/function/module]

### Changes Made
[Refactor description]

### Behavior Preserved
- [API 1]: ✅
- [API 2]: ✅

### Files Changed
- [file 1]

### Tests
- All tests pass: [yes/no]
- New tests added: [count]

### Verification
| Check | Status |
|-------|--------|
| Public API unchanged | ✅ |
| Tests pass | ✅ |
| Build pass | ✅ |

### Recommendation
[Ready to merge]
```

## Important Principles

### Must preserve
- Function signatures
- Return values
- Error behavior
- Side effects (file I/O, network calls, etc.)
- Performance characteristics

### Can change
- Internal implementation
- Variable names
- Code structure
- Comments
- Helper functions

### Warning
- If refactor affects public API → stop and ask
- If behavior unclear → ask user
- If tests don't cover enough → add tests first

## Notes

- **Primary goal**: preserve behavior
- **Secondary goal**: improve code quality
- If goals conflict → prioritize preserving behavior
- If complex refactor → split into multiple smaller PRs
- Use commands from `CLAUDE.md` → `Project Commands` section
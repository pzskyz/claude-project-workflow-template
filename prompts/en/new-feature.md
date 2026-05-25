---
description: Develop new feature - standard workflow
---

# Develop New Feature

## Environment

You are helping the user develop a new feature. Approach systematically.

## Input

$ARGUMENTS

## Process

### Phase 1: Understand requirements

- [ ] Ask user to clarify:
  - What problem needs to be solved?
  - What should the feature do?
  - Any special constraints or requirements?
- [ ] Summarize and confirm with user

### Phase 2: Survey code

- [ ] Read `CLAUDE.md` to understand project structure
- [ ] Find similar features
- [ ] Trace through existing code
- [ ] Identify 5-10 key files to read

### Phase 3: Ask clarifying questions

- [ ] Identify unclear constraints
- [ ] What edge cases need handling?
- [ ] How should errors be handled?
- [ ] Performance requirements?
- [ ] Backward compatibility?

### Phase 4: Design

- [ ] Propose multiple approaches (if applicable)
- [ ] Analyze trade-offs
- [ ] If user approves → continue

### Phase 5: Implementation

- [ ] Read identified files
- [ ] Implement according to chosen architecture
- [ ] Write tests (read test command from `CLAUDE.md` → `Project Commands`)
- [ ] Run verification pipeline

### Phase 6: Verify

- [ ] Run tests (from `CLAUDE.md`)
- [ ] Run build (from `CLAUDE.md`)
- [ ] Run lint/typecheck (from `CLAUDE.md`)
- [ ] Generate verification report

## Final Output

```markdown
## Verification Report

### Feature
[Feature description]

### Files changed
- [file 1]
- [file 2]

### Tests run
[test command from CLAUDE.md]

### Build status
[pass/fail]

### Lint status
[pass/fail]

### Recommendation
[ready to merge / needs fixes]
```

## Notes

- Follow surgical changes: only modify what's necessary
- Don't "improve" unrelated code
- Match existing patterns in codebase
- If ambiguous → ask user before guessing
- Use commands from `CLAUDE.md` → `Project Commands` section
---
description: Finalize - check diff, docs, save memory
---

# Dev Finalize

Complete development session with final checks.

## Checklist

### 1. Diff Review

```bash
# View all changes
git status --short
git diff --cached
git diff
```

**Check:**
- [ ] Files changed match intent
- [ ] No unexpected changes
- [ ] Changes are surgical, no "improvements"
- [ ] No extra debug code
- [ ] No extra commented-out code

### 2. Test Coverage

Read test command from `CLAUDE.md` → `Project Commands`:

```bash
# Run tests to confirm
{{TEST_COMMAND}}
```

**Check:**
- [ ] All tests pass
- [ ] New tests for new behavior
- [ ] Existing tests not broken

### 3. Documentation

**Check:**
- [ ] Comments updated if logic changed
- [ ] README updated if public API changed
- [ ] Migration docs if schema changed
- [ ] API docs if endpoints changed

### 4. Build Verification

Read build command from `CLAUDE.md` → `Project Commands`:

```bash
# Build to confirm no issues
{{BUILD_COMMAND}}
```

**Check:**
- [ ] Build succeeds
- [ ] No critical warnings

### 5. Memory Update

Save insights to memory system if:
- Important architecture decisions
- New patterns discovered
- Gotchas or caveats
- Lessons learned

## Final Report

```markdown
## Development Complete

### Summary
[One sentence summary of changes]

### Files Changed
- [file 1] - [what changed]
- [file 2] - [what changed]

### Verification Results
| Check | Status |
|-------|--------|
| Tests | ✅ Pass |
| Build | ✅ Pass |
| Lint  | ✅ Pass |
| E2E   | ✅ Pass / N/A |

### Key Decisions
- [Decision 1]
- [Decision 2]

### Next Steps (if any)
- [Action 1]
- [Action 2]

### Recommendation
[Ready to merge / Needs manual review / Blocked]
```

## Rules

- **Never execute literal placeholders** like `{{TEST_COMMAND}}`
- Always read commands from `CLAUDE.md` first
- If command is unknown, inspect project files or ask user

## When Manual Review is Needed

- High-risk changes (auth, payment, database)
- Breaking changes
- Large refactors
- Security-sensitive code
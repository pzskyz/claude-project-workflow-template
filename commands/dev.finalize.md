---
description: Finalize - check diff, docs, save memory
---

# Dev Finalize

Complete development session with final checks.

## Rules

- Use the verification results from `/dev.verify`.
- If verification has not been run yet, run `/dev.verify` first.
- Do not re-run expensive checks unless necessary.

## Checklist

### 1. Diff Review

```bash
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

Confirm tests pass from verification results.

**Check:**
- [ ] New tests for new behavior
- [ ] Existing tests not broken

### 3. Documentation

**Check:**
- [ ] Comments updated if logic changed
- [ ] README updated if public API changed
- [ ] Migration docs if schema changed
- [ ] API docs if endpoints changed

### 4. Build Status

Confirm build succeeded from verification results.

### 5. Memory Update

Save insights to memory if:
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
| Tests | ✅ Pass / ❌ Fail |
| Build | ✅ Pass / ❌ Fail |
| Lint | ✅ Pass / ❌ Fail / N/A |
| E2E | ✅ Pass / ❌ Fail / N/A |

### Risks / Skipped Checks
- [any concerns or skipped checks]

### Recommendation
[Ready to merge | Needs manual review | Blocked]
```

## When Manual Review is Needed

- High-risk changes (auth, payment, database)
- Breaking changes
- Large refactors
- Security-sensitive code
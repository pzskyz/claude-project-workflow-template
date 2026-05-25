---
description: Orchestrate complete workflow from analyze to finalize
---

# Dev Full Pipeline

Execute complete development workflow: analyze → implement → verify → finalize.

<!-- IMPORTANT: Replace {{PLACEHOLDERS}} with actual project commands. -->
<!-- If a placeholder is not replaced, do not execute it. Inspect project files to find the correct command. If no command can be found, mark it as UNKNOWN and ask the user. -->

## Workflow Overview

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Analyze   │ →  │  Implement  │ →  │   Verify    │ →  │  Finalize   │
│  Understand │    │  Make       │    │  Run tests  │    │  Summarize  │
│  problem    │    │  changes    │    │  Build/Lint │    │  Report     │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
```

## Phase 1: Analyze

### Goal
- Understand requirements clearly
- Identify impacted files
- Trace current flow
- Propose approach

### Actions

1. **Read CLAUDE.md** (if exists)
   ```bash
   cat CLAUDE.md 2>/dev/null || echo "No CLAUDE.md found"
   ```

2. **Explore codebase**
   ```bash
   # Project structure
   ls -la
   find . -maxdepth 2 -type d | head -15

   # Find related files
   find . -name "*.ts" -o -name "*.tsx" -o -name "*.py" | xargs grep -l "PATTERN" 2>/dev/null
   ```

3. **Trace flow**
   - Identify entry point
   - Follow code path
   - Identify dependencies

4. **Create analysis report**
   ```markdown
   ## Analysis Report

   ### Problem
   [Describe the issue to solve]

   ### Current Flow
   [Trace through current code]

   ### Root Cause (if bug)
   [Hypothesis about cause]

   ### Impacted Files
   - [file 1]
   - [file 2]

   ### Proposed Approach
   [Suggest approach]

   ### Test Plan
   - [Unit tests to add/modify]
   - [Integration tests if needed]

   ### Risk Level
   - Low / Medium / High

   ### Verification Level
   - [0/1/2/3]
   ```

5. **Wait for user approval** before implementing

## Phase 2: Implement

### Goal
- Make surgical changes
- Keep unrelated behavior intact
- Write/update tests

### Actions

1. **Read files to modify**
   ```bash
   cat [file1]
   cat [file2]
   ```

2. **Implement changes**
   - Follow existing patterns
   - Keep changes surgical
   - Add comments if needed

3. **Update/create tests**
   ```bash
   # Run test to confirm test written correctly
   {{TEST_COMMAND}}
   ```

4. **Stage changes**
   ```bash
   git add [changed files]
   ```

## Phase 3: Verify

### Goal
- Ensure code works correctly
- Build succeeds
- No regressions

### Actions

1. **Run verification at appropriate level**

   **Level 1 (Surgical):**
   ```bash
   {{TEST_COMMAND}}
   {{LINT_COMMAND}}
   ```

   **Level 2 (Feature):**
   ```bash
   {{TEST_COMMAND}}
   {{BUILD_COMMAND}}
   {{LINT_COMMAND}}
   ```

   **Level 3 (Cross-system):**
   ```bash
   {{TEST_COMMAND}}
   {{BUILD_COMMAND}}
   {{E2E_COMMAND}}
   ```

2. **Fix any issues**
   - If test fails → fix test or fix code
   - If build fails → fix compilation errors
   - If lint fails → fix style issues

3. **Re-verify** after fixing

## Phase 4: Finalize

### Goal
- Review final diff
- Ensure only necessary changes
- Report results

### Actions

1. **Review diff**
   ```bash
   git diff --cached
   git diff
   ```

2. **Check cleanup**
   - No extra debug code
   - No commented-out code
   - No extra TODOs/FIXMEs

3. **Generate final report**
   ```markdown
   ## Final Report

   ### What Changed
   [Describe changes]

   ### Files Modified
   - [file 1]
   - [file 2]

   ### Tests
   - Added: [count]
   - Modified: [count]
   - All passing: [yes/no]

   ### Verification
   - Build: [pass/fail]
   - Lint: [pass/fail]
   - E2E: [pass/fail/N/A]

   ### Risks
   - [any concerns or skipped checks]

   ### Recommendation
   [ready to merge / needs manual review]
   ```

4. **Save memory** if new insights
   - Architecture decisions
   - Patterns discovered
   - Lessons learned

## Customization markers

<!-- CUSTOMIZE: Update commands for project -->

Placeholders to replace:
- `{{TEST_COMMAND}}` - Test runner command
- `{{BUILD_COMMAND}}` - Build command
- `{{LINT_COMMAND}}` - Lint command
- `{{E2E_COMMAND}}` - E2E command

## Flags

### --analyze-only
Run only Phase 1 (Analyze), no implementation.

### --skip-e2e
Skip E2E tests in Phase 3.

### --level=1|2|3
Force verification level (instead of auto-detect).
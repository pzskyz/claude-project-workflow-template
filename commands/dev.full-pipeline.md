---
description: Orchestrate complete workflow from analyze to finalize
---

# Dev Full Pipeline

Run the complete workflow using project commands from `CLAUDE.md`.

## Pipeline

1. Analyze → 2. Approval gate → 3. Implement → 4. Verify → 5. E2E if needed → 6. Finalize

## Phase 1 — Analyze

- Read `CLAUDE.md`
- Inspect relevant files
- Classify risk level
- Identify impacted files
- Create or update `.claude-analysis.md`
- Define test plan
- Define verification level

**Stop after analysis** unless the user explicitly requested autonomous execution.

## Phase 2 — Implement

- Follow `.claude-analysis.md`
- Make surgical changes only
- Add/update tests for behavior changes

## Phase 3 — Verify

Run `/dev.verify`.

## Phase 4 — E2E

Run `/dev.e2e` if:
- verification level is 3
- user-facing behavior changed
- auth/API/routing/database/payment flow changed

## Phase 5 — Finalize

Run `/dev.finalize`.

## Rules

- Read `CLAUDE.md` first.
- Use commands from `CLAUDE.md` → `Project Commands`.
- Never execute literal placeholders.
- Follow coding rules from `CLAUDE.md`.

## Flags

### --analyze-only
Run only Phase 1 (Analyze), no implementation.

### --skip-e2e
Skip E2E tests in Phase 4.

### --level=1|2|3
Force verification level (instead of auto-detect).
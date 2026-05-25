# Claude Project Workflow Template

Reusable starter kit for any Claude Code project.

## Structure

```
claude-project-workflow-template/
├── README.md                 # Vietnamese setup guide
├── README.en.md              # English setup guide
├── CLAUDE.template.md        # Main template (copy to new projects)
├── commands/                 # Slash commands (English only)
│   ├── dev.analyze.md        # Analyze codebase (read-only)
│   ├── dev.verify.md         # Run test/build/lint
│   ├── dev.e2e.md            # E2E testing
│   ├── dev.full-pipeline.md  # Complete workflow
│   └── dev.finalize.md       # Summary & memory
└── prompts/                  # Prompt templates
    ├── vi/                   # Vietnamese prompts
    │   ├── bug-fix.md
    │   ├── new-feature.md
    │   ├── refactor.md
    │   └── verify-only.md
    └── en/                   # English prompts
        ├── bug-fix.md
        ├── new-feature.md
        ├── refactor.md
        └── verify-only.md
```

## Quick Start

### 1. Copy to a new project

```bash
# Create commands directory
mkdir -p .claude/commands

# Copy main template
cp claude-project-workflow-template/CLAUDE.template.md ./CLAUDE.md

# Copy all commands
cp claude-project-workflow-template/commands/*.md .claude/commands/

# Copy prompts (optional)
cp claude-project-workflow-template/prompts/en/*.md .claude/prompts/
```

### 2. Customize for your project

#### Step 1: Update CLAUDE.md

Open `CLAUDE.md` and replace placeholders:

```markdown
{{PROJECT_NAME}}         → Your project name
{{FRAMEWORK}}            → Next.js, React, FastAPI, etc.
{{TEST_COMMAND}}         → npm test, pytest, cargo test
{{BUILD_COMMAND}}        → npm run build
{{LINT_COMMAND}}         → npm run lint, ruff check .
{{E2E_COMMAND}}          → npx playwright test, npm run e2e
```

#### Step 2: Update dev.verify.md

Open `.claude/commands/dev.verify.md` and replace commands in the `<!-- CUSTOMIZE: -->` section.

Examples:
- Next.js:
  ```bash
  npm run lint
  npm run typecheck
  npm test
  npm run build
  ```
- Python:
  ```bash
  pytest
  ruff check .
  mypy .
  ```
- Monorepo:
  ```bash
  cd packages/backend && npm run test
  cd packages/frontend && npm run test
  ```

### 3. Test the workflow

```bash
# Verify Claude reads CLAUDE.md
# Type: "/dev.verify" - Claude will run verification

# Or run full pipeline
# Type: "/dev.full-pipeline"
```

## Workflow

```
1. Analyze      → Understand codebase, no code changes
2. Implement    → Make surgical changes
3. Verify       → Run test/build/lint based on level
4. Finalize     → Summary, diff check, memory save
```

## Verification Levels

| Level | When             | Checks              |
| ----- | ---------------- | ------------------- |
| 0     | Docs/config only | Check formatting    |
| 1     | Surgical fix     | Unit tests + lint   |
| 2     | Feature change   | Tests + build       |
| 3     | Cross-system     | Tests + build + E2E |

## Advanced Customization

### Add new commands

Create a file in `.claude/commands/`:

```markdown
---
description: Command description
---

# Command Name

Command content...
```

### Create custom prompts

Create a file in `.claude/prompts/` with frontmatter:

```markdown
---
description: Prompt description
---

# Prompt Title

Prompt content...
```

## Important Notes

**Placeholder Safety Rule**: If a `{{PLACEHOLDER}}` is not replaced, DO NOT execute it. Inspect project files to find the correct command. If no command can be found, mark it as UNKNOWN and ask the user.

## Links

- [CLAUDE.md](./CLAUDE.template.md) - Main template
- [dev.verify.md](./commands/dev.verify.md) - Verification command
- [dev.full-pipeline.md](./commands/dev.full-pipeline.md) - Complete workflow
# Claude Project Workflow Template

Reusable starter kit for any Claude Code project. Only `CLAUDE.md` needs customization; all other files copy as-is.

## Structure

```
claude-project-workflow-template/
├── README.md                 # Vietnamese setup guide
├── README.en.md              # English setup guide
├── CLAUDE.template.md        # Main template (copy to new projects)
├── commands/                 # Slash commands (English)
│   ├── dev.analyze.md        # Analyze codebase (read-only)
│   ├── dev.verify.md        # Run verification
│   ├── dev.e2e.md           # E2E testing
│   ├── dev.full-pipeline.md # Complete workflow
│   └── dev.finalize.md       # Summary
└── prompts/                  # Prompt templates
    ├── vi/                   # Vietnamese
    │   ├── bug-fix.md
    │   ├── new-feature.md
    │   ├── refactor.md
    │   └── verify-only.md
    └── en/                   # English
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

# Copy CLAUDE template
cp claude-project-workflow-template/CLAUDE.template.md ./CLAUDE.md

# Copy all commands
cp claude-project-workflow-template/commands/*.md .claude/commands/

# Copy prompts (optional)
cp claude-project-workflow-template/prompts/en/*.md .claude/prompts/
```

### 2. Only customize CLAUDE.md

Open `CLAUDE.md` and fill in your project information:

#### Project Overview & Tech Stack
```markdown
## Project Overview
[Describe project]

## Tech Stack
- **Framework**: Next.js
- **Language**: TypeScript
...
```

#### Project Commands (Source of truth)
```markdown
## Project Commands

| Purpose | Command | Notes |
|---|---|---|
| Setup | `npm install` | Install dependencies |
| Test | `npm test` | Run test suite |
| Build | `npm run build` | Production build |
| Lint | `npm run lint` | Static linting |
| E2E | `npx playwright test` | End-to-end tests |
```

**Important**: Commands in `CLAUDE.md` are the single source of truth. Other commands read from here.

### 3. Test workflow

```bash
# Verify Claude reads CLAUDE.md
# Type: "/dev.verify" - Claude will run verification

# Or run full pipeline
# Type: "/dev.full-pipeline"
```

## Principles

### Single Source of Truth

```
CLAUDE.md → Project Commands (source of truth)
commands/*.md → Read from CLAUDE.md
prompts/*.md → Task templates, no specific commands
```

### Command Resolution Rules

1. Read `CLAUDE.md` first
2. Use commands from `Project Commands` section
3. Never execute literal placeholders like `{{TEST_COMMAND}}`
4. If command is `UNKNOWN`, inspect project files:
   - `package.json`
   - `pyproject.toml`
   - `Makefile`
   - `README.md`
5. If still unknown, ask the user

## Workflow

```
1. Analyze      → Understand codebase, no code changes
2. Implement    → Make surgical changes
3. Verify       → Run test/build/lint based on level
4. Finalize     → Summary, diff check, memory save
```

## Verification Levels

| Level | When | Checks |
|-------|------|--------|
| 0 | Docs/config only | Manual review |
| 1 | Surgical fix | Targeted tests + lint/typecheck |
| 2 | Feature change | Tests + build + lint/typecheck |
| 3 | Cross-system | Tests + build + E2E |

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

## Links

- [CLAUDE.md](./CLAUDE.template.md) - Main template
- [dev.verify.md](./commands/dev.verify.md) - Verification command
- [dev.full-pipeline.md](./commands/dev.full-pipeline.md) - Complete workflow
---
description: Analyze codebase - read-only, no code changes
---

# Dev Analyze

Analyze the codebase to understand structure, patterns, and relationships. No code changes.

## Purpose

- Understand project architecture
- Identify key files
- Trace execution flow
- Find patterns and conventions
- Recommend approach for next task

## Process

### Step 1: Read CLAUDE.md (if exists)

```bash
cat CLAUDE.md 2>/dev/null || echo "No CLAUDE.md found"
```

### Step 2: Explore structure

```bash
# View directory structure
ls -la
tree -L 2 -I node_modules 2>/dev/null || find . -maxdepth 2 -type d | head -20

# Find key files
find . -maxdepth 3 -name "*.md" -o -name "*.json" | grep -E "(package|README|tsconfig)" | head -10
```

### Step 3: Identify tech stack

```bash
# Check package manager
ls package.json pyproject.toml Cargo.toml go.mod composer.json 2>/dev/null

# Check framework
grep -r "from " --include="*.py" | head -5 2>/dev/null
grep -r "import " --include="*.ts" | head -5 2>/dev/null
```

### Step 4: Find key files

```bash
# Find entry points
find . -maxdepth 3 \( -name "main.py" -o -name "index.ts" -o -name "app.ts" -o -name "main.go" \) 2>/dev/null

# Find routes/controllers
find . -maxdepth 3 \( -name "routes*" -o -name "controllers*" -o -name "pages*" \) -type d 2>/dev/null

# Find test files
find . -maxdepth 3 -name "*.test.*" -o -name "*_test.py" 2>/dev/null | head -10
```

### Step 5: Analyze patterns

- Read key files to understand coding style
- Identify architecture pattern (MVC, layered, microservices, etc.)
- Find common utilities/helpers
- Evaluate test coverage

## Output

Provide a report with:

1. **Project Overview**
   - Project name, purpose
   - Tech stack
   - Architecture pattern

2. **Directory Structure**
   - Main directories and their purposes
   - Entry points

3. **Key Files** (5-10 files)
   - File name
   - Purpose
   - Relationships to other files

4. **Patterns and Conventions**
   - Coding style
   - Naming conventions
   - Testing approach
   - Error handling pattern

5. **Recommendations**
   - Approach for specific task
   - Files to read first
   - Cautions (code needing care)

## Example Output

```markdown
## Analysis Report

### Project Overview
- **Name**: MyApp
- **Type**: Next.js web application
- **Purpose**: E-commerce platform

### Tech Stack
- Next.js 14 (App Router)
- TypeScript
- Prisma + PostgreSQL
- Tailwind CSS

### Key Files
1. `app/page.tsx` - Homepage
2. `app/api/products/route.ts` - Product API
3. `lib/prisma.ts` - Database client
4. `components/ProductCard.tsx` - Product display

### Recommendations
- Follow App Router conventions
- Use Prisma client from `lib/prisma.ts`
- Test API routes with mock headers
```

## Notes

- Analyze only, DO NOT modify code
- If ambiguous cases arise, ask the user
- Provide concrete file paths, not vague descriptions
- If project has its own CLAUDE.md, read it first
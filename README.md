# Claude Project Workflow Template

Bộ template dùng lại cho mọi project Claude Code. Chỉ cần customize `CLAUDE.md`, các file khác copy nguyên.

## Cấu trúc

```
claude-project-workflow-template/
├── README.md                 # Hướng dẫn setup (Tiếng Việt)
├── README.en.md             # Setup guide (English)
├── CLAUDE.template.md        # Template chính (copy sang project mới)
├── commands/                 # Slash commands (tiếng Anh)
│   ├── dev.analyze.md        # Phân tích codebase (read-only)
│   ├── dev.verify.md        # Chạy verification
│   ├── dev.e2e.md           # E2E testing
│   ├── dev.full-pipeline.md # Toàn bộ workflow
│   └── dev.finalize.md      # Tổng kết
└── prompts/                  # Prompt templates
    ├── vi/                   # Tiếng Việt
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

## Cách sử dụng

### 1. Copy sang project mới

```bash
# Tạo thư mục commands trong project mới
mkdir -p .claude/commands

# Copy CLAUDE template
cp claude-project-workflow-template/CLAUDE.template.md ./CLAUDE.md

# Copy tất cả commands
cp claude-project-workflow-template/commands/*.md .claude/commands/

# Copy prompts (tùy chọn)
cp claude-project-workflow-template/prompts/en/*.md .claude/prompts/
```

### 2. Chỉ cần customize CLAUDE.md

Mở `CLAUDE.md` và điền thông tin project của bạn:

#### Project Overview & Tech Stack
```markdown
## Project Overview
[Mo ta project]

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

**Quan trọng**: Commands trong `CLAUDE.md` là source of truth duy nhất. Các commands khác sẽ đọc từ đây.

### 3. Test workflow

```bash
# Kiểm tra Claude đọc CLAUDE.md
# Gõ: "/dev.verify" - Claude sẽ chạy verification

# Hoặc chạy full pipeline
# Gõ: "/dev.full-pipeline"
```

## Nguyên tắc

### Single Source of Truth

```
CLAUDE.md → Project Commands (source of truth)
commands/*.md → Đọc từ CLAUDE.md
prompts/*.md → Mẫu giao việc, không chứa command
```

### Command Resolution Rules

1. Đọc `CLAUDE.md` trước
2. Sử dụng commands từ `Project Commands` section
3. Không execute literal placeholders như `{{TEST_COMMAND}}`
4. Nếu command là `UNKNOWN`, inspect project files:
   - `package.json`
   - `pyproject.toml`
   - `Makefile`
   - `README.md`
5. Nếu vẫn không tìm được, hỏi user

## Quy trình làm việc

```
1. Analyze      → Hiểu codebase, không sửa code
2. Implement    → Làm thay đổi surgical
3. Verify       → Chạy test/build/lint theo level
4. Finalize     → Tổng kết, kiểm tra diff, lưu memory
```

## Verification Levels

| Level | Khi nào | Checks |
|-------|---------|--------|
| 0 | Docs/config only | Manual review |
| 1 | Surgical fix | Targeted tests + lint/typecheck |
| 2 | Feature change | Tests + build + lint/typecheck |
| 3 | Cross-system | Tests + build + E2E |

## Tùy chỉnh nâng cao

### Thêm command mới

Tạo file trong `.claude/commands/`:

```markdown
---
description: Mô tả command
---

# Command Name

Nội dung command...
```

### Tạo prompt riêng

Tạo file trong `.claude/prompts/` với frontmatter:

```markdown
---
description: Mô tả prompt
---

# Prompt Title

Nội dung prompt...
```

## Liên kết

- [CLAUDE.md](./CLAUDE.template.md) - Template chính
- [dev.verify.md](./commands/dev.verify.md) - Verification command
- [dev.full-pipeline.md](./commands/dev.full-pipeline.md) - Full workflow
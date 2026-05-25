# Claude Project Workflow Template

Bộ template dùng lại cho mọi project Claude Code.

## Cấu trúc

```
claude-project-workflow-template/
├── README.md                 # Hướng dẫn setup (Tiếng Việt)
├── README.en.md             # Setup guide (English)
├── CLAUDE.template.md        # Template chính (copy sang project mới)
├── commands/                 # Slash commands (tiếng Anh)
│   ├── dev.analyze.md        # Phân tích codebase (read-only)
│   ├── dev.verify.md        # Chạy test/build/lint
│   ├── dev.e2e.md           # E2E testing
│   ├── dev.full-pipeline.md # Toàn bộ workflow
│   └── dev.finalize.md      # Tổng kết
└── prompts/                  # Prompt templates
    ├── vi/                   # Tiếng Việt
    │   ├── bug-fix.md       # Sửa lỗi
    │   ├── new-feature.md   # Phát triển tính năng mới
    │   ├── refactor.md      # Tái cấu trúc
    │   └── verify-only.md   # Chỉ xác minh
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

### 2. Customize cho project của bạn

#### Bước 1: Cập nhật CLAUDE.md

Mở `CLAUDE.md` và thay thế các placeholder:

```markdown
{{PROJECT_NAME}}         → Tên project của bạn
{{FRAMEWORK}}            → Next.js, React, FastAPI, v.v.
{{TEST_COMMAND}}         → npm test, pytest, cargo test
{{BUILD_COMMAND}}        → npm run build
{{LINT_COMMAND}}         → npm run lint, ruff check .
{{E2E_COMMAND}}          → npx playwright test, npm run e2e
```

#### Bước 2: Cập nhật dev.verify.md

Mở `.claude/commands/dev.verify.md` và thay thế commands trong phần `<!-- CUSTOMIZE: -->`.

Ví dụ Next.js:
```bash
npm run lint
npm run typecheck
npm run test
npm run build
```

Ví dụ Python:
```bash
pytest
ruff check .
mypy .
```

Ví dụ Monorepo:
```bash
cd packages/backend && npm run test
cd packages/frontend && npm run test
```

### 3. Test workflow

```bash
# Kiểm tra Claude đọc CLAUDE.md
# Gõ: "/dev.verify" - Claude sẽ chạy verification

# Hoặc chạy full pipeline
# Gõ: "/dev.full-pipeline"
```

## Quy trình làm việc

```
1. Analyze      → Hiểu codebase, không sửa code
2. Implement    → Làm thay đổi surgical
3. Verify       → Chạy test/build/lint theo level
4. Finalize     → Tổng kết, kiểm tra diff, lưu memory
```

## Verification Levels

| Level | Khi nào          | Check gì            |
| ----- | ---------------- | ------------------- |
| 0     | Docs/config only | Check formatting    |
| 1     | Surgical fix     | Unit tests + lint   |
| 2     | Feature change   | Tests + build       |
| 3     | Cross-system     | Tests + build + E2E |

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
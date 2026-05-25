---
description: Chỉ xác minh - chạy verification cho changes hiện tại
---

# Verify Only - Chỉ Xác minh

## Môi trường làm việc

Chỉ chạy verification cho changes hiện tại. KHÔNG sửa code trừ khi người dùng yêu cầu.

## Yêu cầu đầu vào

$ARGUMENTS

## Quy trình

### Bước 1: Xem thay đổi

```bash
git status --short
git diff --name-only
git diff
```

### Bước 2: Xác định affected area

- [ ] Xác định files thay đổi
- [ ] Xác định loại thay đổi:
  - Docs/config only?
  - Bug fix?
  - Feature?
  - Cross-system?
- [ ] Đánh giá risk level

### Bước 3: Chọn verification level

| Level | Khi nào | Checks |
|-------|---------|--------|
| 0 | Docs/config only | Manual review |
| 1 | Surgical fix | Targeted tests + lint/typecheck |
| 2 | Feature change | Tests + build + lint/typecheck |
| 3 | Cross-system | Tests + build + E2E |

### Bước 4: Chạy verification

Đọc commands từ `CLAUDE.md` → `Project Commands`.

- Không execute literal placeholders như `{{TEST_COMMAND}}`
- Sử dụng commands từ CLAUDE.md
- Nếu command không xác định được, inspect project files

### Bước 5: Report kết quả

## Output

```markdown
## Verification Report

### Changes Summary
- **Files**: [count]
- **Type**: [docs/config/bug/feature/refactor]
- **Scope**: [surgical/feature/cross-system]

### Verification Level
[0/1/2/3]

### Commands Run
- [command] — [pass/fail/skipped]

### Build / Quality Status
- Tests: [pass/fail/skipped]
- Build: [pass/fail/skipped]
- Lint: [pass/fail/skipped]
- E2E: [pass/fail/skipped]

### Issues Found
- [none / list of issues]

### Recommendation
[Ready to merge / Needs fixes / Manual review required]
```

## Nguyên tắc

- KHÔNG sửa code trong quá trình verify
- Nếu thấy lỗi → báo cáo nhưng không tự fix
- Nếu scope không rõ → hỏi người dùng
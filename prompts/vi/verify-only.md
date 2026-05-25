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
# Xem status
git status --short

# Xem danh sách files
git diff --name-only

# Xem chi tiết diff
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

| Level | Khi nào          | Checks              |
| ----- | ---------------- | ------------------- |
| 0     | Docs/config only | Check formatting    |
| 1     | Surgical fix     | Unit tests + lint   |
| 2     | Feature change   | Tests + build       |
| 3     | Cross-system     | Tests + build + E2E |

### Bước 4: Chạy verification

**Level 0:**
```bash
# Check formatting
<!-- CUSTOMIZE: prettier, markdownlint, etc. -->
```

**Level 1:**
```bash
# Run tests
{{TEST_COMMAND}}

# Run lint
{{LINT_COMMAND}}
```

**Level 2:**
```bash
# Run tests
{{TEST_COMMAND}}

# Run build
{{BUILD_COMMAND}}

# Run lint
{{LINT_COMMAND}}
```

**Level 3:**
```bash
# Run tests
{{TEST_COMMAND}}

# Run build
{{BUILD_COMMAND}}

# Run E2E
{{E2E_COMMAND}}
```

### Bước 5: Report kết quả

## Output: Verification Report

```markdown
## Verification Report

### Changes Summary
- **Files**: [count]
- **Type**: [docs/config/bug/feature/refactor]
- **Scope**: [surgical/feature/cross-system]

### Verification Level
[0/1/2/3]

### Checks Run

| Check | Command             | Status                |
| ----- | ------------------- | --------------------- |
| Tests | `{{TEST_COMMAND}}`  | ✅ Pass / ❌ Fail       |
| Build | `{{BUILD_COMMAND}}` | ✅ Pass / ❌ Fail / N/A |
| Lint  | `{{LINT_COMMAND}}`  | ✅ Pass / ❌ Fail / N/A |
| E2E   | `{{E2E_COMMAND}}`   | ✅ Pass / ❌ Fail / N/A |

### Results
<!-- Paste test output, build output -->

### Issues Found
- [none / list of issues]

### Skipped Checks
- [any skipped and why]

### Recommendation
[Ready to merge / Needs fixes / Manual review required]
```

## Khi nào skip checks

- Không có E2E command → note và skip
- Không có build step → skip
- Changes là docs-only → skip tests

## Lưu ý

- KHÔNG sửa code trong quá trình verify
- Nếu thấy lỗi → báo cáo nhưng không tự fix
- Nếu tests fail → mô tả rõ lỗi và suggest fix approach
- Nếu unclear scope → hỏi người dùng
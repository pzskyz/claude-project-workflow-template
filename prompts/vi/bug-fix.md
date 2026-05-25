---
description: Sửa lỗi - workflow chuẩn
---

# Sửa Lỗi (Bug Fix)

## Môi trường làm việc

Bạn đang giúp người dùng sửa một lỗi. Hãy tiếp cận theo hướng có hệ thống.

## Yêu cầu đầu vào

$ARGUMENTS

## Quy trình

### Giai đoạn 1: Reproduce lỗi

- [ ] Xác nhận lỗi:
  - **Mô tả actual behavior**: [Dán mô tả]
  - **Expected behavior**: [Dán expected]
- [ ] Reproduce nếu có thể:
  ```bash
  # Chạy command gây ra lỗi
  [command]
  ```
- [ ] Thu thập logs, error messages, screenshots nếu có

### Giai đoạn 2: Trace flow

- [ ] Đọc CLAUDE.md
- [ ] Tìm entry point của flow có lỗi
- [ ] Trace qua các files:
  ```bash
  grep -rn "FUNCTION_NAME" --include="*.ts" --include="*.py"
  ```
- [ ] Xác định root cause hypothesis

### Giai đoạn 3: Analyze

- [ ] Tạo `.claude-analysis.md`:
  ```markdown
  ## Bug Analysis

  ### Problem
  [Mô tả ngắn]

  ### Current Flow
  1. [Step 1]
  2. [Step 2]
  ...

  ### Root Cause Hypothesis
  [Giả thuyết 1]
  [Giả thuyết 2]

  ### Evidence
  - [Log line 1]
  - [Error message]

  ### Test Plan
  - Unit test: [mô tả]
  - Manual test: [các bước]

  ### Impacted Files
  - [file 1]
  - [file 2]

  ### Risk Level
  [Low/Medium/High]

  ### Verification Level
  [1/2/3]
  ```

- [ ] Xác nhận root cause với người dùng

### Giai đoạn 4: Implement fix

- [ ] Đọc files liên quan
- [ ] Apply fix:
  - Surgical changes only
  - Không refactor lung tung
  - Match existing patterns
- [ ] Viết/update tests để cover bug

### Giai đoạn 5: Verify

- [ ] Reproduce lỗi → confirm đã fix
- [ ] Chạy tests:
  ```bash
  {{TEST_COMMAND}}
  ```
- [ ] Chạy lint/build nếu cần:
  ```bash
  {{LINT_COMMAND}}
  {{BUILD_COMMAND}}
  ```

### Giai đoạn 6: Finalize

- [ ] Review diff:
  ```bash
  git diff
  ```
- [ ] Đảm bảo chỉ thay đổi cần thiết
- [ ] Generate verification report

## Output cuối cùng

```markdown
## Bug Fix Verification Report

### Bug
[Tiêu đề ngắn]

### Root Cause
[Mô tả root cause]

### Fix Applied
[Mô tả cách fix]

### Files Changed
- [file 1]
- [file 2]

### Tests
- New test: [Mô tả]
- All tests passing: [yes/no]

### Verification
| Check          | Status |
| -------------- | ------ |
| Bug reproduced | ✅      |
| Bug fixed      | ✅      |
| Tests pass     | ✅      |
| Build pass     | ✅      |

### Recommendation
[Ready to merge]
```

## Ghi chú

- Ưu tiên reproduce lỗi trước khi fix
- Nếu không reproduce được → hỏi người dùng thêm context
- Fix phải cover edge cases, không chỉ happy path
- Sau fix → confirm lỗi không còn
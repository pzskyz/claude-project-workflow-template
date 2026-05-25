---
description: Tái cấu trúc code - giữ nguyên behavior
---

# Tái cấu trúc (Refactor)

## Môi trường làm việc

Bạn đang giúp người dùng refactor code. Mục tiêu: cải thiện structure mà KHÔNG thay đổi behavior.

## Yêu cầu đầu vào

$ARGUMENTS

## Quy trình

### Giai đoạn 1: Xác định scope

- [ ] Xác định target của refactor:
  - Function/module cần refactor?
  - Vấn đề cần giải quyết?
- [ ] Hỏi người dùng:
  - Tại sao cần refactor? (performance, readability, maintainability?)
  - Có deadline/ràng buộc nào không?
- [ ] Xác định boundaries: cái gì KHÔNG refactor

### Giai đoạn 2: Hiểu current behavior

- [ ] Đọc CLAUDE.md
- [ ] Trace current flow:
  ```bash
  # Tìm files liên quan
  grep -rn "TARGET" --include="*.ts" --include="*.py"
  ```
- [ ] Xác định public API contract cần giữ:
  - Function signatures
  - Return values
  - Side effects
  - Error handling behavior

### Giai đoạn 3: Analyze

- [ ] Tạo `.claude-analysis.md`:
  ```markdown
  ## Refactor Analysis

  ### Target
  [File/function/module cần refactor]

  ### Current State
  - LOC: [số dòng]
  - Complexity: [mô tả]
  - Issues: [danh sách vấn đề]

  ### Behavior to Preserve
  - [API 1]
  - [API 2]
  - [Edge cases]

  ### Proposed Changes
  [Mô tả approach]

  ### Regression Test Plan
  - Test 1: [mô tả]
  - Test 2: [mô tả]

  ### Risk Level
  [Low/Medium/High]

  ### Verification Level
  [1/2/3]
  ```

- [ ] Xác nhận approach với người dùng

### Giai đoạn 4: Implement

- [ ] Đọc current code
- [ ] Implement refactor:
  - Thay đổi internals
  - GIỮ NGUYÊN public API
  - GIỮ NGUYÊN behavior
- [ ] Cập nhật internal tests nếu cần

### Giai đoạn 5: Verify

- [ ] Chạy tất cả tests:
  ```bash
  {{TEST_COMMAND}}
  ```
- [ ] Verify behavior không đổi:
  ```bash
  # Manual test các edge cases
  ```
- [ ] Chạy lint/build:
  ```bash
  {{LINT_COMMAND}}
  {{BUILD_COMMAND}}
  ```

### Giai đoạn 6: Finalize

- [ ] Review diff:
  ```bash
  git diff
  ```
- [ ] Đảm bảo:
  - Public API không đổi
  - Tests vẫn pass
  - Không có breaking changes
- [ ] Generate verification report

## Output cuối cùng

```markdown
## Refactor Verification Report

### Target
[File/function/module]

### Changes Made
[Mô tả refactor]

### Behavior Preserved
- [API 1]: ✅
- [API 2]: ✅

### Files Changed
- [file 1]

### Tests
- All tests pass: [yes/no]
- New tests added: [count]

### Verification
| Check                | Status |
| -------------------- | ------ |
| Public API unchanged | ✅      |
| Tests pass           | ✅      |
| Build pass           | ✅      |

### Recommendation
[Ready to merge]
```

## Nguyên tắc quan trọng

### Phải giữ nguyên
- Function signatures
- Return values
- Error behavior
- Side effects (file I/O, network calls, etc.)
- Performance characteristics

### Có thể thay đổi
- Internal implementation
- Variable names
- Code structure
- Comments
- Helper functions

### Cảnh báo
- Nếu refactor ảnh hưởng public API → dừng và hỏi
- Nếu không rõ behavior → hỏi người dùng
- Nếu tests không cover đủ → thêm tests trước

## Ghi chú

- **Primary goal**: giữ nguyên behavior
- **Secondary goal**: cải thiện code quality
- Nếu hai goals xung đột → ưu tiên giữ nguyên behavior
- Nếu refactor phức tạp → tách thành nhiều PRs nhỏ
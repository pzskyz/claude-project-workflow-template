---
description: Phát triển tính năng mới - workflow chuẩn
---

# Phát triển Tính năng Mới

## Môi trường làm việc

Bạn đang giúp người dùng phát triển một tính năng mới. Hãy tiếp cận theo hướng có hệ thống.

## Yêu cầu đầu vào

$ARGUMENTS

## Quy trình

### Giai đoạn 1: Hiểu yêu cầu

- [ ] Hỏi người dùng để làm rõ:
  - Vấn đề cần giải quyết là gì?
  - Tính năng cần làm gì?
  - Ràng buộc hoặc yêu cầu đặc biệt?
- [ ] Tóm tắt và xác nhận với người dùng

### Giai đoạn 2: Khảo sát code

- [ ] Đọc `CLAUDE.md` để hiểu cấu trúc dự án
- [ ] Tìm các tính năng tương tự
- [ ] Trace qua code hiện tại
- [ ] Xác định 5-10 file quan trọng cần đọc

### Giai đoạn 3: Hỏi rõ

- [ ] Xác định các ràng buộc chưa rõ
- [ ] Edge cases nào cần xử lý?
- [ ] Error handling như thế nào?
- [ ] Performance requirements?
- [ ] Backward compatibility?

### Giai đoạn 4: Thiết kế

- [ ] Đề xuất nhiều hướng tiến (nếu có)
- [ ] Phân tích trade-off
- [ ] Nếu người dùng duyệt → tiếp tục

### Giai đoạn 5: Implementation

- [ ] Đọc các file đã xác định
- [ ] Implement theo architecture đã chọn
- [ ] Viết tests
- [ ] Chạy verification pipeline sử dụng commands từ `CLAUDE.md` → `Project Commands`

### Giai đoạn 6: Xác minh

- [ ] Chạy tests từ `CLAUDE.md`
- [ ] Chạy build từ `CLAUDE.md`
- [ ] Chạy lint/typecheck từ `CLAUDE.md`
- [ ] Generate verification report

## Output cuối cùng

```markdown
## Verification Report

### Tính năng
[Mo ta tính năng]

### Files changed
- [file 1]
- [file 2]

### Tests run
[từ CLAUDE.md → Project Commands]

### Build status
[pass/fail]

### Lint status
[pass/fail]

### Recommendation
[ready to merge / needs fixes]
```

## Ghi chú

- Follow surgical changes: chỉ thay đổi những gì cần thiết
- Không "improve" code không liên quan
- Match existing patterns trong codebase
- Nếu ambiguous → hỏi người dùng trước khi đoán
- Sử dụng commands từ `CLAUDE.md` → `Project Commands` section
# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | TC-48 |
| **REQ liên quan** | REQ-04 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Danh Kiên |
| **Ngày phát hiện** | 21/05/2026 |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
An active member can borrow more than 3 books

**Môi trường:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows 11
- Ngôn ngữ giao diện: English

**Điều kiện tiên quyết:**
Login successfully on active account **ba.nguyen@email.com** and have 3 books borrowed

**Bước tái hiện:**
1. Click on the **Borrow this book** symbol.
2. Confirm borrowing book.

**Kết quả mong đợi:**
Error returned stating a member can only borrow up to 3 books

**Kết quả thực tế:**
Confirm notification **Book borrowed successfully!** pop up

**Tác động:**
Violating the BRD: allowing a member to borrow more than 3 books

**Minh chứng:**
`<!-- Đính kèm ảnh chụp màn hình nếu có -->`
> e.g. ![BUG-01](../../images/kien-bug01.png)

**Đề xuất xử lý:**
`<!-- Gợi ý cách sửa lỗi nếu có -->` 

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | TC-49 |
| **REQ liên quan** | REQ-04 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Danh Kiên |
| **Ngày phát hiện** | 21/05/2026 |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
Suspended member be labeled as expired

**Môi trường:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows 11
- Ngôn ngữ giao diện: English

**Điều kiện tiên quyết:**
Login successfully on suspended account **cu.le@email.com**

**Bước tái hiện:**
1. Click on the **Borrow this book** symbol.
2. Confirm borrowing book.

**Kết quả mong đợi:**
Refused to borrow book for the account is suspended

**Kết quả thực tế:**
Notification **Thành viên đã hết hạn. Không thể mượn sách.**

**Tác động:**
SRS violation: suspended member being labeled as expired

**Minh chứng:**
`<!-- -->`

**Đề xuất xử lý:**
`<!-- -->`

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->

# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Bug ID** | BUG-01 |
| **Related TC** | TC-02 |
| **Related REQ** | REQ-04 |
| **Severity** | High |
| **Finder** | Nguyễn Danh Kiên |
| **Find date** | 21/05/2026 |
| **Status** | Open |

**Title:**
An active member can borrow the fourth book

**Environment:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows 11
- Ngôn ngữ giao diện: English

**Precondition:**
Login successfully on active account **ba.nguyen@email.com** and have 3 books borrowed

**Steps:**
1. Click on the **Borrow this book** symbol.
2. Confirm borrowing book.

**Expected result:**
Error returned stating a member can only borrow up to 3 books

**Actual result:**
Confirm notification **Book borrowed successfully!** pop up, a borrow card for the book appear in the **Borrow / Return**, the book state become **Borrowed**

**Consequence:**
Violating the BRD: allowing a member to borrow more than 3 books
    
**Prove:**
submission/image/kien-bug-01

**Fix suggestion:**
Limit the borrow count to 3

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Bug ID** | BUG-02 |
| **Related TC** | TC-04 |
| **Related REQ** | REQ-04 |
| **Severity** | High |
| **Finder** | Nguyễn Danh Kiên |
| **Find date** | 21/05/2026 |
| **Status** | Open |

**Title:**
Suspended member be labeled as expired

**Environment:**
- Trình duyệt: Chrome 148.0.7778.168
- Hệ điều hành: Windows 11
- Ngôn ngữ giao diện: English

**Precondition:**
Login successfully on suspended account **cu.le@email.com**

**Steps:**
1. Click on the **Borrow this book** symbol.
2. Confirm borrowing book.

**Expected result:**
Refused to borrow book for the account is suspended

**Actual result:**
Notification **Thành viên đã hết hạn. Không thể mượn sách.**

**Consequence:**
SRS violation: suspended member being labeled as expired

**Prove:**
submission/image/kien-bug-02

**Fix suggestion:**
Change the error notification message 

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->

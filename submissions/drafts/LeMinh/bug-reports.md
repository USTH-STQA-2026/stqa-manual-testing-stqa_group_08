# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

---

## BUG-01

| Attribute | Details |
|-----------|---------|
| **Bug ID** | BUG-01 |
| **Related TC** | TC-REQ03-06 |
| **REQ liên quan** | REQ-03 |
| **Mức độ** | Low |
| **Người phát hiện** | Lê Đức Minh |
| **Ngày phát hiện** | 26/05/2026 |
| **Trạng thái** | Open |

**Title:**
Category filter is case-sensitive when entering mixed uppercase/lowercase characters

**Environment:**
- Browser: Chrome 148.0.7778.179 
- Operating System: Windows 11
- UI Language: Vietnamese

**Preconditions:**
User has logged into the system successfully

**Steps to Reproduce:**
1. Open the Book List page
2. Enter category keyword "Kinh tế" into the category filter box
3. Verify that books BOOK007, BOOK014, and BOOK015 are displayed
4. Enter category keyword kinh tế or "KINH TẾ"

**Expected Result:**
The system should return the same results for "Kinh tế", "kinh tế", and "KINH TẾ".

**Actual Result:**
The system only returns correct results for Kinh tế.
Inputs "kinh tế" and "KINH TẾ" returns message "Không tìm thấy sách nào.".

**Impact:**
Category filtering behavior is inconsistent and does not support case-insensitive input, causing incorrect search/filter results for users.

**Evidence:**
> ![BUG-01](images/leminh-bug01.png)

**Suggested Fix:**
Normalize category input and database comparison to case-insensitive matching before filtering results.

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `<!-- TC-xx -->` |
| **REQ liên quan** | `<!-- REQ-xx -->` |
| **Mức độ** | `<!-- High / Medium / Low -->` |
| **Người phát hiện** | `<!-- Họ tên thành viên -->` |
| **Ngày phát hiện** | `<!-- DD/MM/YYYY -->` |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
`<!-- Mô tả hành vi lỗi -->`

**Bước tái hiện:**
1. `<!-- -->`
2. `<!-- -->`
3. `<!-- -->`

**Kết quả mong đợi:**
`<!-- -->`

**Kết quả thực tế:**
`<!-- -->`

**Tác động:**
`<!-- -->`

**Minh chứng:**
`<!-- -->`

**Đề xuất xử lý:**
`<!-- -->`

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->

# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | TC-08 |
| **REQ liên quan** | REQ-08 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Vân Khánh |
| **Ngày phát hiện** | 20/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
Member look up others' book records

**Môi trường:**
- Trình duyệt: Chrome 148.0.7778.179
- Hệ điều hành: Windows 11
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
- Login successful as ba.nguyen@email.com
- `MEM004` is a valid Member ID belonging to another member in the DB.

**Bước tái hiện:**
1. Go to “**Search borrow records**”.
2. Enter `MEM004` into the search field.
3. Click “**Search**”.

**Kết quả mong đợi:**
Not allowed to view other members' borrow records.

**Kết quả thực tế:**
Display record `BR003` of member Hoàng Cá Biệt.

**Tác động:**
Violates the BRD: Borrow records are not secured, allowing members to view others’ borrow records.

**Minh chứng:**
![BUG-01](../../images/vkhanh-bug-01.png)

**Đề xuất xử lý:**
- Add an **authorization check**. If the account role is Member, the system must only allow them to view their own data. If they try to enter another member's ID, the backend must block the request and return an error.
- For **Members**: Hide the search input field completely. When they open the page, the system should automatically load and display their personal borrow records.
- For **Librarians**: Keep the search input field visible so they can look up any member as usual. 

---

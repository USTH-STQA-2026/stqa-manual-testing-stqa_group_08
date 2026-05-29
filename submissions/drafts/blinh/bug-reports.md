# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

---

## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | TC-08, TC-11, TC-13 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** |High|
| **Người phát hiện** |  Phí Lê Bảo Linh |
| **Ngày phát hiện** | 28/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
<br> **Add Member**: System incorrectly overrides all validations with generic "Email không hợp lệ" error (Valid, Duplicate, and Empty inputs).

**Môi trường:**
- Trình duyệt: Microsoft Edge 148.0.3967.83
- Hệ điều hành: Windows 11
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:** <br> Logged in as Librarian. Add Member form open.

**Bước tái hiện:**
1. Scenario 1 (TC-08 - **Valid Email**): Fill full name (Nguyễn Linh Tinh), Valid email (linh.ng@email.com), Phone (0987654321). Click"Thêm thành viên".
2. Scenario 2 (TC-11 - **Duplicate Email**): Fill full name (Nguyễn Biết Tuốt), Existing Email (biet.hoang@email.com), Phone (0918273645). Click"Thêm thành viên".
3. Scenario 3 (TC-13 - **Empty Email**): Fill full name (Nguyễn Linh Tinh), Blank email (" "), Phone (0987654321). Click"Thêm thành viên".

**Kết quả mong đợi:** <br> **Scenario 1**: Member created successfully. <br> **Scenario 2**: Error displays: Msg: "Email đã tồn tại." <br> **Scenario 3**: Error displays: Msg: "Email không được để trống."

**Kết quả thực tế:** <br> All 3 scenarios are blocked by the same incorrect format message: Msg: "Email không hợp lệ".

**Tác động:** <br> Core feature is blocked (unable to add members). The system incorrectly shows the same "Invalid email" error for everything (valid, duplicate, or blank emails).

**Minh chứng:** 
<br> Ảnh chụp màn hình: ![BUG-01-TC-08](../../images/linh-BUG-01-TC-08.png), ![BUG-01-TC-11](../../images/linh-BUG-01-TC-11.png), ![BUG-01-TC-13](../../images/linh-BUG-01-TC-13.png)

**Đề xuất xử lý:** <br> 1. Fix the email format rule to correctly accept dots (. ) in the email address (e.g., allow linh.ng@email.com). <br> 2. Change the validation order to: Required Fields -> Format Verification -> Database Check (Duplication). Show a specific error message for each case.

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | TC-10 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** | Medium |
| **Người phát hiện** |  Phí Lê Bảo Linh |
| **Ngày phát hiện** | 28/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
<br> **Add Member**: Validation bypass allows member creation with invalid email format (missing dot in domain).

**Bước tái hiện:**
1. Enter valid full name: Nguyễn Linh Tinh
2. Enter email missing a dot in domain: linhng@email
3. Enter valid phone number: 0987654321
4. Click "Thêm thành viên" button.

**Kết quả mong đợi:** <br> System blocks submission and displays error: Msg: "Email không hợp lệ."

**Kết quả thực tế:** <br> System passes validation and creates the member successfully (New member created successfully).

**Tác động:** <br>
Saves invalid emails, breaking future notifications. It proves validation logic is completely backwards (accepts wrong formats, blocks right ones).

**Minh chứng:**
<br> Ảnh chụp màn hình: ![BUG-02](../../images/linh-BUG-02.png)

**Đề xuất xử lý:** <br>
Update the email check rule to block any email that does not have a dot (.) after the @ symbol

---


# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Does the email exist in the DB? | Yes | `librarian@library.com` | Accepted |
| | No | `noone@email.com` | Notification: "Không tìm thấy thành viên" |
| Is the password valid? | Valid | `admin123` | Accepted |
| | Invalid | `wrongpass` | Notification: "Mật khẩu không đúng" |
| Is the input field empty? | Non-empty | (any value) | Normal processing  |
| | Empty | `""` | Notification "Vui lòng nhập..." |

### IDM — Quản lý thành viên (REQ-07)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Is the full name valid? | Non-empty | Nguyễn Học Bá | Accepted |
| | Empty | "" | Notification: "Họ tên không được để trống." | 
| Is the email valid? | Has  @ and dot (.) in domain | cu.le@email.com | Accepted |  
| | Missing @ | userdomain.com | Notification: "Email không hợp lệ." |
| | Missing dot (.) | user@domain | Notification: "Email không hợp lệ." |
| | Missing both @ and dot | userdomain | Notification: "Email không hợp lệ." |
| | Empty | "" | Notification: "Email không được để trống." |
| | Duplicate email | cu.le@email.com | Notification: "Email đã tồn tại." |
| | String length: within allowed range (1 ≤ L ≤ 255) | cu.le@email.com | Valid |
| | String length: exceeds limit by exactly 1 char (L = 256) | A string of exactly 256 chars | Invalid |
| | String length: exceeds limit significantly (L > 256) | A string of 400 chars | Invalid |
| Is the phone number valid?| Valid | 0923456789 | Accepted | 
| | Non-numeric | abc@123 | Notification: "Số điện thoại không hợp lệ." |
| | Wrong length | 092345678 / 09234567890| Notification: "Số điện thoại không hợp lệ." |
| | Empty | "" | Notification "Số điện thoại không được để trống." |



## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-----|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Login successful | User account exists in system. App is on Login page. | 1. Enter a valid email. <br> 2. Enter the correct password. <br> 3. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: librarian@library.com <br> Password: admin123 | Successfully logged into the "Library - Book Management" interface. | REQ-01 | EP |
| TC-02 | Login with **invalid email** (unregistered) | App is on Login page. | 1. Enter unregistered email. <br> 2. Enter any password. <br> 3. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: damtran@emailcom <br> Password: password123 | Notification: "Không tìm thấy thành viên." | REQ-01 | EP |
| TC-03 | Login with **valid email** but **wrong password**  | User account exists. App is on Login page. | 1. Enter registered email. <br> 2. Enter wrong password. <br> 3. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: dam.tran@email.com <br> Password: password 135 | Notification: "Mật khẩu không đúng." | REQ-01 | EP |
| TC-04 | Login with both **fields empty** | App is on Login page. | 1. Leave both fields blank. <br> 2. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: "" <br> Password: "" | Notification: "Please enter your email and password." | REQ-01 | EP |
| TC-05 | Login with **email empty** but **password filled** | App is on Login page. | 1. Leave email blank. <br> 2. Enter any password. <br> 3. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: "" <br> Password: admin123 | Notification: "Please enter your email and password." | REQ-01 | EP |
| TC-06 | Login with **email filled, password empty** | App is on Login page. | 1. Enter valid email.<br> 2. Leave password blank. <br> 3. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: librarian@library.com <br> Password: "" | Notification: "Please enter your email and password." | REQ-01 | EP |
| TC-07 | Login with **valid email** but using **wrong case** (e.g. uppercase) | Account with lowercase email exists. App is on Login page. | 1. Enter same email in uppercase. <br> 2. Enter correct password. <br> 3. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: Librarian@library.com <br> Password: admin123| Notification: "Không tìm thấy thành viên" | REQ-01 | EP |
| TC-08 | Verify **login succeeds** with **maximum credential lengths** (255-char email, 32-char password) | Login page is open. Valid 255-char account is available. |1. Enter 255-char email. <br> 2. Enter 32-char password. <br> 3. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Email: [255_chars]@email.com <br> Password: [32_characters] | Successfully logged into the "Library - Book Management" interface. | REQ-01 | BVA |
| TC-09 | Verify **login fails** when **credential lengths exceed limits** (256-char email or 33-char password) | Login page is open. | 1. Enter 256-char email or 33-char password. <br> 2. Click the "Sign In" button /Press the "Enter" key on the keyboard. | Case A: Email [256_chars], Pass: Valid. <br> Case B: Email: Valid, Pass: [33_chars]. | Login fails. Validation error displays. No system crash. | REQ-01 | BVA |
| TC-10 | Add member with **all valid inputs** | Logged in as Librarian. Add Member form is open. Email does not already exist. | 1. Enter full name. <br> 2. Enter valid email. <br> 3. Enter phone number.<br> 4. Click the "Add member" button.| Full name: Nguyễn Linh Tinh <br> Email: linh.ng@email.com <br> Phone number: 0987654321 | New member created successfully. Member appears in member list. | REQ-07 | EP |
| TC-11 | Add member with **invalid email — missing @** | Logged in as Librarian. Add Member form is open. | 1. Enter full name. <br> 2. Enter email without @. <br> 3. Enter phone number. 4. Click the "Add member" button. | Full name: Nguyễn Linh Tinh <br> Email: linh.ngemail.com <br> Phone number: 0987654321 | Notification: "invalid email format. Member not created." | REQ-07 | EP |
| TC-12 | Verify validation fails for email **without any dot** | Logged in as Librarian. Add Member form is open. | 1. Enter full name. <br> 2. Enter email "username@domain". <br> 3. Enter phone number. <br> 4. Click the "Add member" button. | Full name: Nguyễn Linh Tinh <br> Email: linhng@email <br> Phone number: 0987654321 | Notification: "invalid email (no dots). Member not created." | REQ-07 | EP |
| TC-13 | Verify validation fails for email with **dot ONLY in local part** | Logged in as Librarian. Add Member form is open. | 1. Enter full name. 2. Enter email "user.name@domain". 3. Enter phone number. 4. Click the "Add member" button. | Full name: Nguyễn Linh Tinh <br> Email: linh.ng@email <br> Phone number: 0987654321 | Notification: "invalid email (no dot in domain part). Member not created." | REQ-07 | EP |
| TC-14 | Add member with **duplicate email** | Logged in as Librarian. Email already exists in system. Add Member form is open. | 1. Enter full name. 2. Enter an email that already exists. 3. Enter phone number. 4. Click the "Add member" button. | Full name: Nguyễn Biết Tuốt <br> Email: biet.hoang@email.com <br> Phone number: 0918273645 | Notification: "email already exists / duplicate email. Member not created." | REQ-07 | EP |
| TC-15 | Add member with **empty full name** | Logged in as Librarian. Add Member form is open. | 1. Leave full name blank. 2. Enter valid email. 3. Enter phone number. 4. Click the "Add member" button. | Full name: "" <br> Email: linh.ng@email.com <br> Phone number: 0987654321 | Notification: "full name is required. Member not created." | REQ-07 | EP |
| TC-16 | Add member with **empty email** | Logged in as Librarian. Add Member form is open. | 1.Enter full name. 2. Leave email blank. 3. Enter phone number. 4. Click the "Add member" button. | Full name: Nguyễn Linh Tinh <br> Email: "" <br> Phone number: 0987654321 | Notification: "email is required. Member not created." | REQ-07 | EP |
| TC-17 | Add member with **all fields empty** | Logged in as Librarian. Add Member form is open. | 1. Leave all fields blank. 2.Click the "Add member" button. | Full name: "" <br> Email: "" <br> Phone number: "" | Error messages displayed for all required fields. | REQ-07 | EP |
| TC-18 | Verify **non-Librarian** cannot access "Add Member" | Logged in as a non-Librarian role. Navigate to "Library — Book Management". | 1. Login with non-Librarian account. 2. Attempt to access Add Member function.| Account: Member | Access to the "Add Member" option is denied. No form is displayed. | REQ-07 | EP |
| TC-19 | Verify email with subdomain is accepted | Logged in as Librarian. Add Member form is open. | 1. Enter full name. 2. Enter email with subdomain. 3. Enter phone number. 4. Click the "Add member" button. | Full name: Nguyễn Linh Tinh <br> Email: linh.ng@user.email.com <br> Phone number: 0987654321 | Member is added successfully. The email is accepted as valid. | REQ-07 | EP |
| TC-20 | Verify adding a member succeeds with maximum email length (255 chars) | Logged in as Librarian. Valid 255-char account is available. | 1. Fill form with valid data. <br> 2. Enter a 255-char email. <br> 3. Click the "Add member" button. | Email: [255_chars]@email.com | Member created | REQ-07 | BVA |
| TC-21 | Verify adding a member fails when email exceeds limit (256 chars) | Logged in as Librarian. Add Member form open. | 1. Fill form with valid data. <br> 2. Enter a 256-char email. <br> 3. Click the "Add member" button. | Email: [256_chars]@email.com | Action blocked. Error displays. No system crash.  | REQ-07 | BVA |

---------
## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Login | 9 | REQ-01 | EP, BVA |
| Member Management | 12 | REQ-07 | EP, BVA |
| **Tổng** | 21 | 2 | 2 |

# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Is the email valid? | Valid | `librarian@library.com` | Accepted |
| | Invalid | `noone@email.com` | Msg: "Không tìm thấy thành viên" |
| | Case-sensitive | `Librarian@library.com` | Msg: "Không tìm thấy thành viên" |
| Is the password valid? | Valid | `admin123` | Accepted |
| | Invalid | `wrongpass` | Msg: "Mật khẩu không đúng" |
| Is the input field empty? | Non-empty | (any value) | Normal processing  |
| | Empty | `" "` | Msg "Vui lòng nhập..." |

### IDM — Quản lý thành viên (REQ-07)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Is the full name valid? | Non-empty | `Nguyễn Học Bá` | Accepted |
| | Empty | `" "` | Msg: "Họ tên không được để trống." | 
| Is the email valid? | Has  @ and dot (.) in domain | `user@domain.com` | Accepted |  
| | Missing @ | `userdomain.com` | Msg: "Email không hợp lệ." |
| | Missing dot (.) | `user@domain` | Msg: "Email không hợp lệ." |
| | Missing both @ and dot | `userdomain` | Msg: "Email không hợp lệ." |
| | Empty | `" "` | Msg: "Email không được để trống." |
| | Duplicate email | `cu.le@email.com`| Msg: "Email đã tồn tại." |
| | String length: within allowed range (1 ≤ L ≤ 255) | `cu.le@email.com` | Valid |
| | String length: exceeds limit by exactly 1 char (L = 256) | A string of exactly 256 chars | Invalid |
| | String length: exceeds limit significantly (L > 256) | A string of 400 chars | Invalid |
| Is the phone number valid?| Valid | `0923456789` | Accepted | 
| | Non-numeric | `abc@123` | Msg: "Số điện thoại không hợp lệ." |
| | Wrong length | `092345678` / `09234567890`| Msg: "Số điện thoại không hợp lệ." |
| | Empty | `" "` | Msg: "Số điện thoại không được để trống." |



## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-----|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Login successful | User account exists in system. App is on Login page. | 1. Enter a valid email. <br> 2. Enter the correct password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `librarian@library.com` <br> Password: `admin123` | Login successful | REQ-01 | EP |
| TC-02 | Login with **invalid email** (unregistered) | App is on Login page. | 1. Enter unregistered email. <br> 2. Enter any password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `damtran@emailcom` <br> Password: `password123` | Msg: "Không tìm thấy thành viên." | REQ-01 | EP |
| TC-03 | Login with **valid email** but **wrong password**  | User account exists. App is on Login page. | 1. Enter registered email. <br> 2. Enter wrong password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `dam.tran@email.com` <br> Password: `password 135` | Msg: "Mật khẩu không đúng." | REQ-01 | EP |
| TC-04 | Login with both **fields empty** | App is on Login page. | 1. Leave both fields blank. <br> 2. Click "Đăng nhập" button/Press "Enter". | Email: `" "` <br> Password: `" "` | Msg: "Vui lòng nhập email và mật khẩu." | REQ-01 | EP |
| TC-05 | Login with **email empty** but **password filled** | App is on Login page. | 1. Leave email blank. <br> 2. Enter any password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `" "` <br> Password: `admin123` | Msg: "Vui lòng nhập email và mật khẩu." | REQ-01 | EP |
| TC-06 | Login with **email filled, password empty** | App is on Login page. | 1. Enter valid email.<br> 2. Leave password blank. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `librarian@library.com` <br> Password: `" "` | Msg: "Vui lòng nhập email và mật khẩu." | REQ-01 | EP |
| TC-07 | Login with **valid email** but using **wrong case** (e.g. uppercase) | Account with lowercase email exists. App is on Login page. | 1. Enter same email in uppercase. <br> 2. Enter correct password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `Librarian@library.com` <br> Password: `admin123`| Msg: "Không tìm thấy thành viên" | REQ-01 | EP |
| TC-08 | Add member with **all valid inputs** | Logged in as Librarian. Add Member form is open. Email does not already exist. | 1. Enter full name. <br> 2. Enter valid email. <br> 3. Enter phone number.<br> 4. Click "Thêm thành viên" button.| Full name: `Nguyễn Linh Tinh` <br> Email: `linh.ng@email.com` <br> Phone number: `0987654321` | New member created successfully. Member appears in member list. | REQ-07 | EP |
| TC-09 | Add member with **invalid email — missing @** | Logged in as Librarian. Add Member form is open. | 1. Enter full name. <br> 2. Enter email without @. <br> 3. Enter phone number. <br> 4. Click "Thêm thành viên" button. | Full name: `Nguyễn Linh Tinh` <br> Email: `linh.ngemail.com` <br> Phone number: `0987654321` | Msg: "Định dạng email không hợp lệ." | REQ-07 | EP |
| TC-10 | Verify validation fails for email **without any dot** | Logged in as Librarian. Add Member form is open. | 1. Enter full name. <br> 2. Enter email without any dot. <br> 3. Enter phone number. <br> 4. Click "Thêm thành viên" button. | Full name: `Nguyễn Linh Tinh` <br> Email: `linhng@email` <br> Phone number: `0987654321` | Msg: "Định dạng email không hợp lệ." | REQ-07 | EP |
| TC-11 | Add member with **duplicate email** | Logged in as Librarian. Email already exists in system. Add Member form is open. | 1. Enter full name. <br> 2. Enter an email that already exists. <br> 3. Enter phone number. <br> 4. Click "Thêm thành viên" button. | Full name: `Nguyễn Biết Tuốt` <br> Email: `biet.hoang@email.com` <br> Phone number: `0918273645` | Msg: "Email đã tồn tại." | REQ-07 | EP |
| TC-12 | Add member with **empty full name** | Logged in as Librarian. Add Member form is open. | 1. Leave full name blank. <br> 2. Enter valid email. <br> 3. Enter phone number. <br> 4. Click "Thêm thành viên" button. | Full name: `" "` <br> Email: `linh.ng@email.com` <br> Phone number: `0987654321` | Msg: "Vui lòng nhập họ tên." | REQ-07 | EP |
| TC-13 | Add member with **empty email** | Logged in as Librarian. Add Member form is open. | 1.Enter full name. <br> 2. Leave email blank. <br> 3. Enter phone number. <br> 4. Click "Thêm thành viên" button. | Full name: `Nguyễn Linh Tinh` <br> Email: `" "` <br> Phone number: `0987654321` | Msg: "Vui lòng nhập email." | REQ-07 | EP |
| TC-14 | Add member with **all fields empty** | Logged in as Librarian. Add Member form is open. | 1. Leave all fields blank. <br> 2.Click "Thêm thành viên" button. | Full name: `" "` <br> Email: `" "` <br> Phone number: `" "` | No action initiated. | REQ-07 | EP |
| TC-15 | Verify **Member** cannot "Thêm thành viên" | Logged in as Member. | Login with Member account. | Account: biet.hoang@email.com | "Thêm thành viên" button not exist . | REQ-07 | EP |
| TC-16 | Verify adding a **member succeeds** with **maximum email length** (255 chars) | Logged in as Librarian. Valid 255-char account is available. | 1. Fill form with valid data. <br> 2. Enter a 255-char email. <br> 3. Click "Thêm thành viên" button. | Email: [255_chars]@email.com | Member created. | REQ-07 | BVA |
| TC-17 | Verify adding a **member fails** when email **exceeds limit** (256 chars) | Logged in as Librarian. Add Member form open. | 1. Fill form with valid data. <br> 2. Enter a 256-char email. <br> 3. Click "Thêm thành viên" button. | Email: [256_chars]@email.com | No action initiated. | REQ-07 | BVA |
| TC-18 | Verify adding a **member fails** when email **over limit** (> 256 chars) | Logged in as Librarian. Add Member form open. | 1. Fill form with valid data. <br> 2. Enter a 257-char email. <br> 3. Click "Thêm thành viên" button. | Email: [257_chars]@email.com | No action initiated. | REQ-07 | BVA |

---------
## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Login | 7 | REQ-01 | EP |
| Member Management | 11 | REQ-07 | EP, BVA |
| **Tổng** | 18 | 2 | 2 |
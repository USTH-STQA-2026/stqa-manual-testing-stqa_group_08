# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Xem danh sách sách (REQ-02)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Does the user have permission to view the book list? | Yes | LIB001 (Librarian) | Display complete book list |
|  | Yes | MEM002 (Member) | Display complete book list |
| Book Status? | Available | Available | Display status as “Có sẵn” |
|  | Borrowed | Borrowed | Display status as “Đang mượn” |
| Is the book information complete? | Complete | Valid Book Data | Display correct book information |
|  | Incomplete | NULL field (title/author/category) | Display default value |
| Is the publication year valid? | Valid | 2020 | Display correct publication year |
|  | Below minimum value | 999 | Display default value |
| Is there a real-time status update event? | Borrow event | Borrow Event | Update status to “Đang mượn” immediately |
|  | Return event | Return Event | Update status to “Có sẵn” immediately |


| `<!-- tự điền -->` | | | |

### IDM — Tìm kiếm và lọc sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

---

## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-REQ02-01 | Verify that a librarian can view the complete book list | User account librarian@library.com / admin123 is active | Login with librarian account. Navigate to the Book List page | Email: librarian@library.com Password: admin123 | Display all 20 books with correct information including title, author, category, publication year, and status | REQ-02 | EP |
| TC-REQ02-02 | Verify that a borrowed book displays the correct status | User account ba.nguyen@email.com / password123 is active | 1. Login with member account. Open the Book List page. Find book BOOK003 - Kiểm thử phần mềm nhập môn | Book ID: BOOK003 | Display status as “Đang mượn” | REQ-02 | EP |
| TC-REQ02-03 | Verify that an available book displays the correct status | User account dam.tran@email.com / password123 is active | Login with member account. Open the Book List page. Find book BOOK001 - Lập trình Flutter cơ bản | Book ID: BOOK001 | Display status as “Có sẵn” | REQ-02 | EP |
| TC-REQ02-04 | Verify that lost books are displayed correctly | User account librarian@library.com / admin123 is active | Login with librarian account. Open the Book List page. Find book BOOK007 - Kinh tế vi mô | Book ID: BOOK007 | Display status as “Thất lạc” | REQ-02 | EP |
| TC-REQ02-05 | Verify that book information is displayed correctly | User account biet.hoang@email.com / password123 is active | Login with member account Open the Book List page Find book BOOK010 - An toàn thông tin cơ bản | Book ID: BOOK010 | Display correct title, author (Trần Quốc An), category (Công nghệ), publication year (2023), and status (Có sẵn) | REQ-02 | EP | 
| TC-REQ02-06 | Verify real-time status update after borrowing a book | User account ba.nguyen@email.com | User borrows BOOK008 - Mạng máy tính | Borrow Event on BOOK008 | Book status is updated immediately from “Có sẵn” to “Đang mượn” | REQ-02 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |

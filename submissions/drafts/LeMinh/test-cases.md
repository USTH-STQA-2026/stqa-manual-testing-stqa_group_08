# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Xem danh sách sách (REQ-02)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Who can view the book list? | Librarian | LIB001 (Librarian) | Display complete book list |
|  | Member | MEM002 (Member) | Display complete book list |
| Book Status? | Available | BOOK018 | Display status as “Có sẵn” |
|  | Borrowed | BOOK002 | Display status as “Đang mượn” |
|  | Lost | BOOK020 | Display status as "Thất lạc" |
| Is the book information complete? | Complete | BOOK008 | Display information: Mạng máy tính - Lý Văn Tài • Công nghệ - 2022 |
|  | Incomplete | NULL field (title/author/category) | Display missing/incorrect information |
| Is there a real-time status update event? | Borrow event | Msg: "Book borrowed successfully!" | Status changes to "Borrowed" |
|  | Return event | Msg: "Book returned successfully!" | Status changes to "Available" |


### IDM — Tìm kiếm và lọc sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Does the keyword exist in the database? | Yes (book title) | `"Flutter"` | Display books containing "Flutter" |
| | Yes (author name) | `"Nguyễn"` | Display books written by authors containing "Nguyễn" |
| | No | `"XYZ123"` | Display "Không tìm thấy sách nào." |
| Is the search case-sensitive? | Lowercase | `"flutter"` | Same result as "Flutter" |
| | Uppercase | `"FLUTTER"` | Same result as "Flutter" |
| Does the category exist in the database? | Yes | "Kinh tế" | Display books in category "Kinh tế" (BOOK007, BOOK014, BOOK015) | 
| | No | "ABC" |  Display "Không tìm thấy sách nào." | 

---

## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| TC ID | Test objectives | Precondition | Test steps | Input value | Expected result | REQ | Technique |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-REQ02-01 | Verify that a librarian can view the complete book list | Login successful on librarian acccount | Open the Book List page | Email: librarian@library.com / admin123 | Display all 20 books | REQ-02 | EP |
| TC-REQ02-02 | Verify that a member can view the complete book list | Login successful on member acccount | Open the Book List page | Email: dam.tran@email.com / password123 | Display all 20 books | REQ-02 | EP |
| TC-REQ02-03 | Verify that a borrowed book displays the correct status | Login successful with any valid account (Librarian or Member) | Open the Book List page. Find book BOOK003 - Kiểm thử phần mềm nhập môn | Book ID: BOOK003 | Display status as “Đang mượn” | REQ-02 | EP |
| TC-REQ02-04 | Verify that an available book displays the correct status | Login successful with any valid account (Librarian or Member) | Open the Book List page. Find book BOOK001 - Lập trình Flutter cơ bản | Book ID: BOOK001 | Display status as “Có sẵn” | REQ-02 | EP |
| TC-REQ02-05 | Verify that lost books are displayed correctly | Login successful with any valid account (Librarian or Member) | Open the Book List page. Find book BOOK007 - Kinh tế vi mô | Book ID: BOOK007 | Display status as “Thất lạc” | REQ-02 | EP |
| TC-REQ02-06 | Verify that book information is displayed correctly | Login successful with any valid account (Librarian or Member) | Login. Open the Book List page Find book BOOK010 - An toàn thông tin cơ bản | Book ID: BOOK010 | Display correct title, author (Trần Quốc An), category (Công nghệ), publication year (2023), and status (Có sẵn) | REQ-02 | EP |
| TC-REQ02-07 | Verify real-time status update after borrowing a book | Login successful with any valid account (Librarian or Member) | Receive msg: "Book borrowed successfully!" | Borrow Event on BOOK008 | Book status is updated immediately from “Có sẵn” to “Đang mượn” | REQ-02 | EP |
| TC-REQ02-08 | Verify real-time status update after return a book | Login successful with any valid account (Librarian or Member) | Receive msg: "Book returned successfully!" | Return Event on BOOK008 | Book status is updated immediately from “Đang mượn” to “Có sẵn” | REQ-02 | EP |
| TC-REQ03-01 | Verify searching books by title | Login successful with any valid account (Librarian or Member) | Open Book List page. Enter keyword into search box | Flutter | Display BOOK001 - Lập trình Flutter cơ bản | REQ-03 | EP |
| TC-REQ03-02 | Verify searching books by author | Login successful with any valid account (Librarian or Member) | Open Book List page. Enter keyword into search box | Nguyễn | Display books by authors containing Nguyễn (BOOK001, BOOK006, BOOK009, BOOK016) | REQ-03 | EP |
| TC-REQ03-03 | Verify search is case-insensitive | Login successful with any valid account (Librarian or Member) | Open Book List page. Search using lowercase and uppercase keywords | flutter, FLUTTER | Returns the same result as Flutter | REQ-03 | EP |
| TC-REQ03-04 | Verify system handles non-existing keyword | Login successful with any valid account (Librarian or Member) | Open Book List page. Enter keyword into search box | XYZ123 | Display "Không tìm thấy sách nào." | REQ-03 | EP |
| TC-REQ03-05 | Verify filtering books by category | Login successful with any valid account (Librarian or Member) | Open Book List page. Enter category into filter box | Kinh tế | Display only books in category Kinh tế (BOOK007, BOOK014, BOOK015) | REQ-03 | EP |
| TC-REQ03-06 | Verify category filter is case-insensitive | Login successful with any valid account (Librarian or Member) | Open Book List page. Enter category into filter box | kinh tế, KINH TẾ | Returns the same result as Kinh tế (BOOK007, BOOK014, BOOK015) | REQ-03 | EP | 
 
---

## Tổng hợp

| Functional Group | Number of TC | Covered REQ | Applied IDM Techniques |
|----------------|-------|---------|----------------------|
| View Book List | 8 | REQ-02 | EP |
| Search & Filter Books | 6 | REQ-03 | EP |
| **Total** | **14** | REQ-02 REQ-03 | EP |

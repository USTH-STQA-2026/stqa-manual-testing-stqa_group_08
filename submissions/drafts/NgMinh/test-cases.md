# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Trả sách (REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Book status | Being borrowed | BOOK003 | "Trả sách" button available -> Change status to "Có sẵn" after returning |
| | Available | BOOK009 | "Trả sách" button unavailable |
| | Overdue | BOOK013 | "Trả sách" button available -> Change status to "Có sẵn" after returning |
| Overdue date warning | dueDate < currentDate | BOOK013 | Show Warning message:" Đã quá hạn trả sách" |   
| | dueDate > currentDate | BOOK005 | No Warning message |

### IDM — Xử lý sách quá hạn (REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Record status | dueDate < currentDate | BR001(due date 01/09/2024)  | Marked as "Quá hạn" |
| | dueDate < currentDate | BR005 (due date 15/06/2024) -> returned at 20/06/2024 | Return as "Đã trả" + Marked as "Quá hạn" |
| | dueDate > currentDate | BR002 | Return as "Đã trả" |
| Overdue Record checking | Librarian | Check BR001, BR003, BR005 | Able to check all the overdue records |
| | Member |MEM002 check BR001| Anle to check their overdue record |



## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC05-01 |Librarian verifying user not returning book | - Member MEM002 is currently active <br> - Member MEM002 has a borrow record <br> - The book BOOK003 is currently borrowed | - Click "Trả sách" to return book <br> - Check the dueDate and currentDate| Record BR001(MEM002 borrows BOOK003 - due date 15/09/2024) | Marked as "Quá hạn" + Warning message: "Đã quá hạn trả sách" | REQ 05 | Equivalence partitioning |
| TC05-02 |Librarian verifying user returning book late | - Member MEM003 is currently active <br> - Member MEM003 has borrow record <br> - The book BK006 is currently borrowed |  - Click "Trả sách" to return book <br> - Check the dueDate and currentDate | Record BR005(MEM003 borrows BOOK06 - Due date 15/06/2024, returned 20/06/2024) |Return "Đã trả" + Warning message: "Trả sách quá hạn" | REQ 05 | Boundary Value Analysis |
| TC05-03 | LIbrarian verifying expired or suspended user | - Member MEM004 is not currently active - Member MEM004  has no borrow record | - Click "Trả sách" to return book <br> - Check the dueDate and currentDate | Empty record | Display "Không tìm thấy phiếu mượn | REQ 05 | Equivalence partitioning |
| TC06-01 | Librarian marking record as "Quá hạn" | - MEM003 has a borrow record <br> -BR005 is overdue | Search for "MEM003" in "Tra cứu phiếu mượn" category | Record BR005(MEM003 borrows BOOK06 - Due date: 15/06/2024, return date: 20/06/2024) | Return "Quá hạn" and display in Overdue list | REQ 06 | Boundary Value Analysis |
| TC06-02 | Librarian checking all overdue records | - Members have borrow records <br> - The records must be overdue(dueDate < currentDate) | Librarian click on "Kiểm tra sách quá hạn" | Record BR001, BR002, BR003, BR004, BR005, BR006 | Display all the overdue records: BR001, BR003, BR005 | REQ 06 | Equivalence Partitioning |
| TC06-03 | User checking their overdue record | - MEM002 is currently active <br> -MEM002 has a borrow record <br> - Record BR001 must be overdue | - Member click on "Mượn/Trả" <br> - Check the overdue record in "Phiếu mượn của tôi" | Account: ba.nguyen@email.com <br> -Record: BR001( MEM002 borrows BOOK003) | Display the Record BR001 with the "Quá hạn" mark | REQ 06 | Equivalence Partitioning | 

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |

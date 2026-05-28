# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Trả sách (REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Record status | Borrowed (Overdue) | BOOK003 | "Trả sách" button available |
| | Available | BOOK005 | "Trả sách" button unavailable |
| | Borrowed | BOOK013 | "Trả sách" button available  |
| Status after clicking "Trả sách" button| dueDate < currentDate | BOOK003 | Mark as "Đã trả" + Change book status to "Có sẵn" + Warning message:"Trả sách quá hạn" |   
| | dueDate > currentDate | BOOK005 | No Warning message |
| | dueDate > currentDate | BOOK013 | Mark as "Đã trả" + Change book status to "Có sẵn" |

### IDM — Xử lý sách quá hạn (REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Record status after clicking "Kiểm tra sách quá hạn"| dueDate < currentDate | BR001(due date 01/09/2024)  | Return as "Quá hạn" |
| | Book returned | BR005 (due date 15/06/2024) -> returned at 20/06/2024 | Return as "Đã trả"  |
| | dueDate > currentDate | BR003 | Return as "Đang mượn" |
| Overdue Record checking | Librarian | Check BR001, BR003, BR005 | Able to check all the overdue records |
| | Member |MEM002 check BR001| Able to check their overdue record |



## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC05-01 | Checking record BR001 status after clicking "Trả sách" | - MEM002 is currently active <br> - MEM002 has borrow record <br> - BOOK003 is currently borrowed | - Click "Trả sách" to return book <br> - Check the dueDate and currentDate | Record BR001(MEM002 borrows BOOK003 - due date 15/09/2024) | Return as "Đã trả" + Warning message: "Đã quá hạn trả sách" | REQ 05 | Equivalence partitioning |
| TC05-02 | Checking record BR005 status after returning book | - MEM003 is currently active <br> - MEM003 has borrow record <br> - BOOK006 is currently borrowed | - Check the dueDate and currentDate | Record BR005(MEM003 borrows BOOK06 - Due date 15/06/2024, returned 20/06/2024) |Mark as "Đã trả" | REQ 05 | Equivalence partitioning |
| TC05-03 | Checking record BR003 status after clicking "Trả sách" | - MEM006 is currently active <br> - MEM006 has borrow record <br> - BOOK013 is currently borrowed | - Click "Trả sách" to return book <br> - Check the dueDate | Record BR003(MEM006 borrows BOOK013 - due date 15/10/2024) | Mark as "Đã trả" | REQ 05 | Equivalence partitioning |
| TC06-01 | Librarian verifying BR003 "Quá hạn" mark | - MEM006 is currently active <br> - MEM006 is currently borrowing BOOK013 | - Click on "Tra cứu phiếu mượn" <br> - Search for "MEM006" <br> Look at Record BR003 dueDate | BR003( MEM006 borrows BOOK013 - dueDate 15/10/2024) | Return as "Đang mượn" | REQ 06 | Equivalence partitioning |
| TC06-02 | Librarian checking all overdue records | - Members have borrow records <br> - The records must be overdue( dueDate < currentDate ) | Librarian click on "Kiểm tra sách quá hạn" | Record BR001, BR002, BR003, BR004, BR005, BR006 | Display all the overdue records: BR001, BR005 | REQ 06 | Equivalence Partitioning |
| TC06-03 | Member checking their overdue record | - MEM002 is currently active <br> -MEM002 has a borrow record <br> - Record BR001 must be overdue | - Member click on "Mượn/Trả" <br> - Check the overdue record in "Phiếu mượn của tôi" | Account: ba.nguyen@email.com <br> -Record: BR001( MEM002 borrows BOOK003) | Display the Record BR001 with the "Quá hạn" mark | REQ 06 | Equivalence Partitioning | 

---

## Tổng hợp
..
| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |

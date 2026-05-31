# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Trả sách (REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Current record status | Borrowing | BR001 | "Trả sách" button available + Book status: "Đang mượn"|
| | Returned | BR004 | "Trả sách" button unavailable + Book status: "Có sẵn" |
| Return date status | Return on time | BR003 | Successfully returned the book, Mark as "Đã trả" + Change book status to "Có sẵn" + No warning message |  
| | Return late/Haven't returned | BR001 |Successfully returned the book, Mark as "Đã trả" + Change book status to "Có sẵn" + Display warning message:"Trả sách quá hạn" | 

### IDM — Xử lý sách quá hạn (REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Librarian checking record status | Overdue, not checked by librarian | BR001 | Status: "Đang mượn" (DB remain unchanged) |
| | Overdue, checked by librarian | BR001 | Status update to "Quá hạn" |
| | Within due date, checked by librarian | dueDate > currentDate | Status remained "Đang mượn" |
| | Returned, checked by librarian | BR002 | Status remained "Đã trả" |
| List view permission | Librarian | Check BR001, BR003, BR005 | Able to check all the overdue records |
| | Member |MEM002 check BR001| Able to check their overdue record |



## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC05-01 | Return overdue book | - MEM002 is currently active <br> - MEM002 is currently borrowing BOOK003 | - Go to "Mượn/Trả” <br> - Click "Trả sách" at borrow record | BR001 | Return as "Đã trả" + Update book status to "Có sẵn" + Warning message: "Đã quá hạn trả sách" | REQ 05 | Equivalence partitioning |
| TC05-02 | Return book within date | - MEM006 is currently active <br> - MEM006 is currently borrowing BOOK013 | - Go to “Mượn/Trả” <br> - Click "Trả sách" at borrow record | Record BR006(MEM002 borrows BOOK011- due date 13/06/2026) | Return as "Đã trả" + Update book status to "Có sẵn" + Message: "Trả sách thành công" | REQ 05 | Equivalence partitioning |
| TC05-03 | Display "Trả sách" button | - MEM002 is currently active <br> - MEM002 is currently borrowing BOOK003 | Log in account: ba.nguyen@email.comGo into "Mượn/Trả" | BR001 | Able to click "Trả sách" to return book | REQ 05| Equivalence partitioning |
| TC06-01 | Librarian verifying BR003 "Quá hạn" mark | - MEM006 is currently active <br> - MEM006 is currently borrowing BOOK013 | - Click on "Kiểm tra sách quá hạn" <br> - Click on "Tra cứu phiếu mượn" <br> - Search for "MEM006" | BR003( MEM006 borrows BOOK013 - dueDate 15/10/2024) | Return as "Đang mượn" | REQ 06 | Equivalence partitioning |
| TC06-02 | Librarian checking all overdue records | - Members have borrow records <br> - The records must be overdue( dueDate < currentDate ) | Librarian click on "Kiểm tra sách quá hạn" | Record BR001, BR002, BR003, BR004, BR005, BR006 | Display all the overdue records: BR001, BR005 | REQ 06 | Equivalence Partitioning |
| TC06-03 | Member checking their overdue record | - MEM002 is currently active <br> -MEM002 has a borrow record <br> - Record BR001 must be overdue | - Member click on "Mượn/Trả" <br> - Check the overdue record in "Phiếu mượn của tôi" | Account: ba.nguyen@email.com <br> -Record: BR001( MEM002 borrows BOOK003) | Display the Record BR001 with the "Quá hạn" mark | REQ 06 | Equivalence Partitioning | 

---

## Tổng hợp
..
| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |

# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Trả sách (REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|Trạng thái thành viên | Active | MEM002 | Can return book |
| | Expired | MEM005 | Cannot return book |
| | Active | MEM003 | Can return book |
| Hạn trả sách| Havent returned | BOOK003 | Book unavailable -> Warning|   
| |Return late | BOOK006 | Book available -> Warning |
| | Return on time | BOOK001 | Book available |
### IDM — Xử lý sách quá hạn (REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|Trạng thái phiếu mượn| Borrowed, overdue | BR001 (due date 15/9/2024) | Displayed as "Quá hạn" + Warning|
| | Returned, overdue | BR005 (due date 15/06/2024) -> returned at 20/06/2024| Displayed as "Đã trả" + Warning |
| | Borrowed, overdue | BR003 (due date 15/10/2024)| Displayed as "Quá hạn" + Warning|
| Hiện thị chức năng| Review all records | BR001 -> BR005 | Only the librarian can view|
| | Filter overdue records | BR001 & BR003 | Users can filter their overdue records|





## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC05-01 |Verifying user not returning | Member has borrow record | MEM002 borrow B00K03 | Due date 15/09/2024, return after date | Return "Quá hạn" + Warning | REQ 05 | Equivalence partitioning |
| TC05-02 |Verifying user returning late | Member has borrow record| MEM003 borrow BOOK006 | Due date 15/06/, returned 20/06/2024 |Return "Đã trả" + Warning | REQ 05 | Boundary Value Analysis |
| TC05-03 | Verifying user returning on time | Member has borrow record | MEM003 borrow BOOK001 | Due date 24/08/2024, returned 20/08/2024 | Return "Đã trả"| REQ 05 | Equivalence partitioning |
| TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật 
| TC06-02 | Verifying correct record | Borrow record exists | Librarian check due date | BR001(MEM003) due date: 15/06/2024, return date: 20/06/2024 | Return "Quá hạn" and display Overdue list | REQ 06 | Boundary Value Analysis
| TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật 

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |

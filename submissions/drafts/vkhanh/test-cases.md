# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Borrow Record Lookup (REQ-08)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Search ID existence | Valid | `MEM002` | Display borrow records |
| | Wrong casing | `mem002` | Msg: "No borrow records found." |
| | Leading/trailing spaces | `"  MEM002  "` | Msg: "No borrow records found." |
| | Invalid | `ABC123` / `!@#` | Msg: "No borrow records found." |
| | Empty | `" "` | No action initiated |
| View permission | Librarian | - Account: `librarian` <br> - Lookup: `MEM001` | Display records |
| | Member - Lookup personal records | - Account: `ba.nguyen` <br> - Lookup: `MEM001` | Display records |
| | Member - Lookup others' records | - Account: `ba.nguyen` <br> - Lookup: `MEM002` (of another member) | Msg: "Cannot access this borrow record." |
| "Check overdue books" action | Overdue, **not checked** by librarian | `BR001` | Status: "**Borrowing**" (DB unupdated) |
| | Overdue, **checked** by librarian | `BR001` | Status: "**Overdue**" (DB updated) |
| Borrow status | Borrowing | `BR003` | Status: "**Borrowing**" |
| | Returned | `BR002` | Status: "**Returned**" |
| | Overdue | `BR001` | Status: "**Overdue**" |
|Record per member | Multiple records | `MEM003` | Display all records `BR002`, `BR005` |
| | Single record | `MEM006` | Display only 1 record `BR003` |
| | Zero record | `MEM004` | Empty list |

---

## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Librarian lookup valid member (Multiple records) | Login successful as librarian@library.com | 1. Go to “**Search borrow records**”. <br> 2. Enter `MEM003` into the search field. <br> 3. Click “**Search**”. | - Account: librarian@library.com <br> - Search keyword: `MEM003` | Display `BR002`, `BR005` <br> Status: `Returned` | REQ-08 | EP, BVA |
| TC-02 | Wrong casing search keyword | Login successful | 1. Go to “**Search borrow records**”. <br> 2. Enter `mem002` into the search field. <br> 3. Click “**Search**”. | - Account: librarian@library.com <br> - Search keyword: `mem002` | Msg: "No borrow records found." | REQ-08 | EP |
| TC-03 | Leading/trailing spaces search keyword | Login successful | 1. Go to “**Search borrow records**”. <br> 2. Enter `"  MEM002  "` into the search field. <br> 3. Click "**Search**”. | - Account: librarian@library.com <br> - Search keyword: `"  MEM002  "` | Msg: "No borrow records found." | REQ-08 | EP |
| TC-04 | Invalid search keyword | Login successful | 1. Go to "**Search borrow records**”. <br> 2. Enter `ABC123 / !@#` into the search field. <br> 3. Click "**Search**”. | - Account: librarian@library.com <br> - Search keyword: `ABC123 / !@#` | Msg: "No borrow records found." | REQ-08 | EP |
| TC-05 | Empty search keyword | Login successful | 1. Go to "**Search borrow records**”. <br> 2. Enter `" "` into the search field. <br> 3. Click "**Search**”. | - Account: librarian@library.com <br> - Search keyword: `" "` | No action initiated | REQ-08 | EP, BVA |
| TC-06 | Member look up personal info (Single record) | Login successful as biet.hoang@email.com | 1. Go to "**Search borrow records**”. <br> 2. Enter `MEM006` into the search field. <br> 3. Click "**Search**”. | - Account: biet.hoang@email.com <br> - Search keyword: `MEM006` | Display `BR003` <br> Status: `Borrowing` | REQ-08 | EP, BVA |
| TC-07 | Member look up personal info (Zero record) | Login successful as cu.le@email.com | 1. Go to “**Search borrow records**”. <br> 2. Enter `MEM004` into the search field. <br> 3. Click “**Search**”. | - Account: cu.le@email.com <br> - Search keyword: `MEM004` | Empty list | REQ-08 | EP, BVA |
| TC-08 | Member look up others' info | Login successful as ba.nguyen@email.com | 1. Go to “**Search borrow records**”. <br> 2. Enter `MEM004` into the search field. <br> 3. Click “**Search**”. | - Account: ba.nguyen@email.com <br> - Search keyword: `MEM004` | Msg: "Cannot access this borrow record." | REQ-08 | EP |
| TC-09 | Overdue book - Not checked by librarian | Login successful as librarian@library.com | Go to “**Borrow / Return**”. | - Account: librarian@library.com <br> - Record ID: `BR001` | Status: "**Borrowing**" (DB unupdated) | REQ-08 | EP |
| TC-10 | Overdue book - Checked by librarian | Login successful as librarian@library.com | 1. Go to “**Borrow / Return**”. <br> 2. Click “**Check overdue books**”. | - Account: librarian@library.com <br> - Record ID: `BR001` | Status: "**Overdue**" (DB updated) | REQ-08 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Borrow Record Lookup | 10 | REQ-08 | EP, BVA |
| **Tổng** | **<!-- ≥ 20 -->** | | |

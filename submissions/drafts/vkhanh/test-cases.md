# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Borrow Record Lookup (REQ-08)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Search ID existence | Valid | `MEM002` | Display borrow records with full details: **Record ID**, **Book Title**, **Borrow Date**, **Due Date**, **Status**. |
| | Wrong casing | `mem002` | Msg: "No borrow records found." |
| | Leading/trailing spaces | `"  MEM002  "` | Msg: "No borrow records found." |
| | Invalid | `ABC123` / `!@#` | Msg: "No borrow records found." |
| | Empty | `" "` | No action initiated |
| View permission | Librarian | - Account: `librarian` <br> - Lookup: `MEM001` | Display borrow records with full details.|
| | Member - Lookup personal records | - Account: `ba.nguyen` <br> - Lookup: `MEM001` | Display borrow records with full details. |
| | Member - Lookup others' records | - Account: `ba.nguyen` <br> - Lookup: `MEM002` (of another member) | Msg: "Cannot access this borrow record." |
| Borrow status | Borrowing | `BR003` | Display full details with Status: "**Borrowing**". |
| | Returned | `BR002` | Display full details with Status: "**Returned**". |
| | Overdue | `BR001` | Display full details with Status: "**Overdue**". |
|Record per member | Multiple records | `MEM003` | Display all records `BR002`, `BR005`, each containing full details. |
| | Single record | `MEM006` | Display only 1 record `BR003` with full details. |
| | Zero record | `MEM004` | Empty list |

---

## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | **Librarian** lookup **valid member** (Multiple records) | - Login successful as librarian. <br> - Member `MEM003` has multiple borrow records (min 2 books) in the DB. | 1. Go to “**Tra cứu phiếu mượn**”. <br> 2. Enter *Search keyword* into the search field. <br> 3. Click “**Tra cứu**”. | - Account: `librarian@library.com` <br> - Search keyword: `MEM003` | Display record `BR002`, `BR005` with: <br> - Record ID: BR002 / BR005 <br> - Member: Trần Dựa Dẫm <br> - Status: **Đã trả** <br> - Book Title, Borrow Date, Due Date: Correctly display as recorded in the system. | REQ-08 | EP, BVA |
| TC-02 | **Wrong casing** search keyword | - Login successful with any valid account (Librarian or Member) <br> - Member `MEM002` has at least 1 borrow record in the DB. | 1. Go to “**Tra cứu phiếu mượn**”. <br> 2. Enter *Search keyword* into the search field. <br> 3. Click “**Tra cứu**”. | - Account: `librarian@library.com` <br> - Search keyword: `mem002` | Msg: "Không tìm thấy phiếu mượn." | REQ-08 | EP |
| TC-03 | Leading/trailing spaces search keyword | - Login successful with any valid account (Librarian or Member) <br> - Member MEM002 has at least 1 borrow record in the DB. | 1. Go to “**Tra cứu phiếu mượn**”. <br> 2. Enter *Search keyword* into the search field. <br> 3. Click “**Tra cứu**”. | - Account: `librarian@library.com` <br> - Search keyword: "  `MEM002`  " | Msg: "Không tìm thấy phiếu mượn." | REQ-08 | EP |
| TC-04 | **Invalid** search keyword | Login successful with any valid account (Librarian or Member) | 1. Go to “**Tra cứu phiếu mượn**”. <br> 2. Enter *Search keyword* into the search field. <br> 3. Click “**Tra cứu**”. | - Account: `librarian@library.com` <br> - Search keyword: `ABC123` | Msg: "Không tìm thấy phiếu mượn." | REQ-08 | EP |
| TC-05 | **Empty** search keyword | Login successful with any valid account (Librarian or Member) | 1. Go to “**Tra cứu phiếu mượn**”. <br> 2. Enter *Search keyword* into the search field. <br> 3. Click “**Tra cứu**”. | - Account: `librarian@library.com` <br> - Search keyword: `" "` | No action initiated | REQ-08 | EP, BVA |
| TC-06 | Member look up **personal info** (Zero record) | - Login successful as `cu.le@email.com` <br> - Member `cu.le` (ID: MEM004) has never borrowed a book in the DB. | 1. Go to “**Tra cứu phiếu mượn**”. <br> 2. Enter *Search keyword* into the search field. <br> 3. Click “**Tra cứu**”. | - Account: `cu.le@email.com` <br> - Search keyword: `MEM004` | Empty list | REQ-08 | EP, BVA |
| TC-07 | Member look up **others' info** | - Login successful as `ba.nguyen@email.com` <br> - `MEM006` is a valid Member ID belonging to another member in the DB. | 1. Go to “**Tra cứu phiếu mượn**”. <br> 2. Enter *Search keyword* into the search field. <br> 3. Click “**Tra cứu**”. | - Account: `ba.nguyen@email.com` <br> - Search keyword: `MEM006` | Empty list | REQ-08 | EP |
| TC-08 | Verify *Overdue* status display | - Login successful with any valid account (Librarian or Member) <br> - The librarian has checked overdue books, and `BR001` is marked as “**Overdue**”. | 1. Go to “**Mượn / Trả**” tab. <br> 2. Locate *Record ID* | - Account: `librarian@library.com` <br> - Record ID: `BR001` | Display record `BR001` with: <br> - Record ID: BR001 <br> - Member: Nguyễn Học Bá <br> - Status: **Quá hạn** <br> - Book Title, Borrow Date, Due Date: Correctly display as recorded in the system. | REQ-08 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Borrow Record Lookup | 9 | REQ-08 | EP, BVA |
| **Tổng** | **<!-- ≥ 20 -->** | | |

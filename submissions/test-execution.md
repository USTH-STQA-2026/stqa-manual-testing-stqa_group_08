# Test Execution 

| Information | |
|---|---|
| **Group** | GROUP 8 |
| **Created Date** | 25/05/2026 |
| **Browser** | Chrome 148.0.7778.179 |
| **Operating System** | Windows 11 |

---

## Detail results

### REQ-01 — Login

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Login | Login successful | Login successful. Access the system. | Pass | | | 
| TC-02 | Login | Msg: "Không tìm thấy thành viên." | Msg: "Không tìm thấy thành viên." | Pass | | |
| TC-03 | Login | Msg: "Mật khẩu không đúng." |  Msg: "Mật khẩu không đúng." | Pass | | |
| TC-04 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |
| TC-05 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |
| TC-06 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |

### REQ-02 — View Book List

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | View Book List | Display all 20 books for librarian account | System displayed all 20 books correctly | Pass | | |
| TC-02 | View Book List | Display all 20 books for member account | System displayed all 20 books correctly | Pass | | |
| TC-03 | View Book List | Display status as “Đang mượn” | BOOK003 displayed status “Đang mượn” correctly | Pass | | |
| TC-04 | View Book List | Display status as “Có sẵn” | BOOK001 displayed status “Có sẵn” correctly | Pass | | |
| TC-05 | View Book List | Display status as “Thất lạc” | BOOK007 displayed status “Thất lạc” correctly | Pass | | |
| TC-06 | View Book List | Display correct book information | BOOK010 information displayed correctly | Pass | | |
| TC-07 | View Book List | Status updates to “Đang mượn” immediately | Status updated immediately | Pass | | |
| TC-08 | View Book List | Status updates to “Có sẵn” immediately | Status updated immediately | Pass | | |

### REQ-03 — Search & Filter Books

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Search & Filter Books | Display BOOK001 when searching “Flutter” | Search returned BOOK001 correctly | Pass | | |
| TC-02 | Search & Filter Books | Display books by authors containing “Nguyễn” | System returned BOOK001, BOOK006, BOOK009, BOOK016 | Pass | | |
| TC-03 | Search & Filter Books | Lowercase and uppercase search return same result | “flutter” and “FLUTTER” returned the same result as “Flutter” | Pass | | |
| TC-04 | Search & Filter Books | Display “Không tìm thấy sách nào.” | System displayed “Không tìm thấy sách nào.” correctly | Pass | | |
| TC-05 | Search & Filter Books | Display only books in category “Kinh tế” | System displayed BOOK007, BOOK014, BOOK015 correctly | Pass | | |
| TC-06 | Search & Filter Books | Category filter is case-insensitive | “kinh tế” and “KINH TẾ” returned different results from "Kinh tế" | Fail | ![BUG-01](../bug-evidence/leminh-bug-01.png) | BUG-01 |

### REQ-04 — Borrow Book

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Borrow Book | Book borrowed successfully on active account not at the borrow limit | Book borrowed successfully on active account not at the borrow limit | Pass | | |
| TC-02 | Borrow Book | Fail to borrow book on active account at the borrow limit | Book borrow successfully | Fail | [BUG-02](../bug-evidence/kien-bug-02.png) | BUG-02 |
| TC-03 | Borrow Book | Fail to borrow book on suspended account with the reason of being suspended | System displayed message for expired account instead of suspended account | Fail | [BUG-03](../bug-evidence/kien-bug-03.png) | BUG-03 |
| TC-04 | Borrow Book | Fail to borrow book on expired account with the reason of being expired | Error notification state that member cannot borrow book for being expired | Pass | | |
| TC-05 | Borrow Book | Due date being 14 days after the borrow date | Due date being 14 days after the borrow date | Pass | | |
| TC-06 | Borrow Book | Unable to borrow borrowed books | Unable to borrow borrowed books | Pass | | |
| TC-07 | Borrow Book | Unable to borrow lost books | Unable to borrow lost books | Pass | | |

### REQ-05 — Return Book

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Return Book | "**Trả sách**" button display right | "**Trả sách**" button display right  | Pass | | |
| TC-02 | Return Book | Update record and book status, display warning message. | Do not have warning message | Fail | [BUG-04](../bug-evidence/Dminh-bug-04.png) | BUG-04 |
| TC-03 | Return Book | Update record and book status, display confirm message. | Book return successfully | Pass | | | 

### REQ-06 — Overdue Handling

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Overdue Handling | Borrow record status remains “Đang mượn”. | Borrow record status remains “Đang mượn”. | Pass | | |
| TC-02 | Overdue Handling | Correct status is displayed for each record type. | Correct status is displayed for each record type. | Pass | | |
| TC-03 | Overdue Handling | Display overdue records `BR001`, `BR003` | Display overdue records `BR001`, `BR003` | Pass | | | 
| TC-04 | Overdue Handling | Display overdue record `BR001` | Display overdue record `BR001` | Pass | | | 

### REQ-07 — Member Management

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Member Management | New member created successfully. | Msg: "Email không hợp lệ" | Fail | [BUG-06-1](../bug-evidence/blinh-bug-06-1.png) | BUG-06 |
| TC-02 | Member Management | Msg: "Email không hợp lệ." | Msg: "Email không hợp lệ." | Pass | | |
| TC-03 | Member Management | Msg: "Email không hợp lệ." | New member created successfully. | Fail | [BUG-05-1](../bug-evidence/blinh-bug-05-1.png) <br> [BUG-05-2](../bug-evidence/blinh-bug-05-2.png) | BUG-05 |
| TC-04 | Member Management | Msg: "Email đã tồn tại." | System triggers format error before duplicate check: "Email không hợp lệ." | Fail | [BUG-06-2](../bug-evidence/blinh-bug-06-2.png) | BUG-06 |
| TC-05 | Member Management | Msg: "Email không được để trống." | System triggers format error before empty check: "Email không hợp lệ." | Fail | [BUG-06-3](../bug-evidence/blinh-bug-06-3.png) | BUG-06 |
| TC-06 | Member Management | Msg: "Họ tên không được để trống." | Msg: "Họ tên không được để trống." | Pass | | |
| TC-07 | Member Management | Msg: "Số điện thoại không được để trống." | Msg: "Email không hợp lệ." | Blocked | | BUG-06 |
| TC-08 | Member Management | Msg: "Họ tên không được để trống." | Msg: "Họ tên không được để trống." (Successfully blocked) | Pass | | |
| TC-09 | Member Management | "Thêm thành viên" button does not exist. | "Thêm thành viên" button does not exist. | Pass | | |

### REQ-08 — Borrow Record Lookup

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Borrow Record Lookup | Display record `BR002`, `BR005` with full information. | Display record `BR002`, `BR005` with full information. | Pass |  |  |
| TC-02 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-03 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-04 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-05 | Borrow Record Lookup | No action initiated | No action initiated | Pass |  |  |
| TC-06 | Borrow Record Lookup | Empty list | Empty list | Pass |  |  |
| TC-07 | Borrow Record Lookup | Not allowed to view other members' borrow records. | Display record `BR003` of member Hoàng Cá Biệt | Fail | [BUG-07](../bug-evidence/vkhanh-bug-07.png) | BUG-07 |
| TC-08 | Borrow Record Lookup | Display record `BR003` with full information. | Display record `BR003` with full information. Status is `Quá hạn` | Pass |  |  |

---

## Test Summary

| Metric | Value |
|--------|---------|
| Total number of test cases | 51 |
| Pass | 41 |
| Fail | 9 |
| Blocked | 1 |
| Not Run | 0 |
| **Pass Rate** | 80.39% |

### Results by Functional Group

| Group | Total TCs | Pass | Fail | Pass Rate |
|------|---------|------|------|------------|
| Login                 | 6 | 6 | 0 | 100% |
| View Book List        | 8 | 8 | 0 | 100% |
| Search & Filter Books | 6 | 5 | 1 | 83.33% |
| Borrow Book           | 7 | 5 | 2 | 71.43% |
| Return Book           | 3 | 2 | 1 | 66.67% |
| Overdue Handling      | 4 | 4 | 0 | 100%   |
| Member Management     | 9 | 4 | 4 | 44.44% |
| Borrow Record Lookup  | 8 | 7 | 1 | 87.5% |
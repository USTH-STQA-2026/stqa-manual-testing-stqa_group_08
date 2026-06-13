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
| TC-01 | Login | Login successful. AppBar displays username and role | Login successful. AppBar displays "Nguyễn Thủ Thư (Thủ Thư)" and "Đăng xuất" | Pass | | | 
| TC-02 | Login | Msg: "Không tìm thấy thành viên." | Msg: "Không tìm thấy thành viên." | Pass | | |
| TC-03 | Login | Msg: "Mật khẩu không đúng." |  Msg: "Mật khẩu không đúng." | Pass | | |
| TC-04 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |
| TC-05 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |
| TC-06 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |

### REQ-02 — View Book List

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | View Book List | Display all 20 books with full details | System displayed all 20 books correctly with full details | Pass | | |
| TC-02 | View Book List | Each book status displayed correctly: "Có sẵn", "Đang mượn", "Thất lạc" | BOOK001: “Có sẵn” <br> BOOK003: “Đang mượn” <br> BOOK007: “Thất lạc” | Pass | | |

### REQ-03 — Search & Filter Books

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Search & Filter Books | Display all books containing "**Flutter**" in title | Display book "**Lập trình Flutter cơ bản**" | Pass | | |
| TC-02 | Search & Filter Books | Display books by authors containing “Nguyễn” | Display books BOOK001, BOOK006, BOOK009, BOOK016 | Pass | | |
| TC-03 | Search & Filter Books | Same as TC-01 regardless of letter casing | Same as TC-01 | Pass | | |
| TC-04 | Search & Filter Books | Display “Không tìm thấy sách nào.” | Display “Không tìm thấy sách nào.” | Pass | | |
| TC-05 | Search & Filter Books | Display only books in category “Kinh tế” | System displayed BOOK007, BOOK014, BOOK015 | Pass | | |
| TC-06 | Search & Filter Books | Same as TC-05 regardless of letter casing | Msg: "Không tìm thấy sách nào." — category filter is case-sensitive | Fail | [BUG-01](bug-evidence/leminh-bug-01.png) | BUG-01 |

### REQ-04 — Borrow Book

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Borrow Book | Borrow successful; new record created; book status: "Đang mượn" | Borrow successful; new record created; book status updated to "Đang mượn" | Pass | | |
| TC-02 | Borrow Book | Reject borrowing. Error msg stating member has reached the 3-book limit; book remains "Có sẵn" | Book borrowed successfully — limit not enforced | Fail | [BUG-02](bug-evidence/kien-bug-02.png) | BUG-02 |
| TC-03 | Borrow Book | Reject borrowing. Msg: "Thành viên đã tạm ngưng. Không thể mượn sách." | System displayed message for expired account instead of suspended account | Fail | [BUG-03](bug-evidence/kien-bug-03.png) | BUG-03 |
| TC-04 | Borrow Book | Reject borrowing. Msg: "Thành viên đã hết hạn. Không thể mượn sách." | Msg: "Thành viên đã hết hạn. Không thể mượn sách." | Pass | | |
| TC-05 | Borrow Book | Due date = borrow date + 14 days | Due date correctly set to borrow date + 14 days | Pass | | |
| TC-06 | Borrow Book | "Mượn sách này" button not shown for borrowed books | "Mượn sách này" button not shown for borrowed book "Quản trị nhân sự hiện đại" | Pass | | |
| TC-07 | Borrow Book | "Mượn sách này" button not shown for lost books | "Mượn sách này" button not shown for lost book "Kinh tế vi mô" | Pass | | |

### REQ-05 — Return Book

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Return Book | "**Trả sách**" button display correctly per record status | "**Trả sách**" button available at BR001 (borrowing); unavailable at BR004 (returned)  | Pass | | |
| TC-02 | Return Book | Record status: "**Đã trả**" <br> Book status: "**Có sẵn**" <br> Warning msg: "**Trả sách quá hạn!**" | Record and book status updated correctly. No warning message displayed | Fail | [BUG-04](bug-evidence/Dminh-bug-04.png) | BUG-04 |
| TC-03 | Return Book | Record status: "**Đã trả**" <br> Book status: "**Có sẵn**" <br> Msg: "**Trả sách thành công**" | Record status: "**Đã trả**" <br> Book status: "**Có sẵn**" <br> Msg: "**Trả sách thành công**" | Pass | | |
| TC-04 | Return Book | Record status: "**Đã trả**" <br> Book status: "**Có sẵn**" <br> Warning msg: "**Trả sách quá hạn!**" | Blocked — precondition unachievable: system does not mark record as overdue when dueDate = currentDate | Fail |  | BUG-04 |

### REQ-06 — Overdue Handling

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Overdue Handling | Borrow record status remains “Đang mượn”. | BR001  status remains “Đang mượn”. | Pass | | |
| TC-02 | Overdue Handling | - BR001 status: "Quá hạn" <br> - BR002 status: "Đã trả" <br> - BR006 status: "Quá hạn" (dueDate = currentDate) <br> - BR007 status: "Đang mượn" (dueDate > currentDate) | - BR001 status: "Quá hạn" <br> - BR002 status: "Đã trả" <br> - BR006 status: "Quá hạn" <br> - BR007 status: "Đang mượn" | Pass |  |  |
| TC-03 | Overdue Handling | All overdue records BR001, BR003 visible to librarian with status "Quá hạn" | Display records BR001, BR003 with status "Quá hạn" | Pass | | | 
| TC-04 | Overdue Handling | Member sees only personal overdue record BR001 with status "Quá hạn" | Display record BR001 with status "Quá hạn" | Pass | | | 

### REQ-07 — Member Management

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Member Management | New member created successfully. | Msg: "Email không hợp lệ" | Fail | [BUG-06-1](bug-evidence/blinh-bug-06-1.png) | BUG-06 |
| TC-02 | Member Management | Msg: "Email không hợp lệ." | Msg: "Email không hợp lệ." | Pass | | |
| TC-03 | Member Management | Msg: "Email không hợp lệ." | New member created successfully. | Fail | [BUG-05-1](bug-evidence/blinh-bug-05-1.png) <br> [BUG-05-2](bug-evidence/blinh-bug-05-2.png) | BUG-05 |
| TC-04 | Member Management | Msg: "Email đã tồn tại." | System triggers format error before duplicate check: "Email không hợp lệ." | Fail | [BUG-06-2](bug-evidence/blinh-bug-06-2.png) | BUG-06 |
| TC-05 | Member Management | Msg: "Email không được để trống." | System triggers format error before empty check: "Email không hợp lệ." | Fail | [BUG-06-3](bug-evidence/blinh-bug-06-3.png) | BUG-06 |
| TC-06 | Member Management | Msg: "Họ tên không được để trống." | Msg: "Họ tên không được để trống." | Pass | | |
| TC-07 | Member Management | Msg: "Số điện thoại không được để trống." | Msg: "Email không hợp lệ." | Blocked | | BUG-06 |
| TC-08 | Member Management | Msg: "Họ tên không được để trống." | Msg: "Họ tên không được để trống." (Successfully blocked) | Pass | | |
| TC-09 | Member Management | "Thành viên" tab and "Thêm thành viên" button are not displayed | "Thành viên" tab and "Thêm thành viên" button are not displayed | Pass | | |
| TC-10 | Member Management | All 6 members displayed with full details: Name, ID, Phone, Borrow count, Status | All 6 members displayed with full details | Pass | | |

### REQ-08 — Borrow Record Lookup

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Borrow Record Lookup | Display record BR002, BR005 with full details. | Display record BR002, BR005 with full details. | Pass |  |  |
| TC-02 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-03 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-04 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-05 | Borrow Record Lookup | No action initiated | No action initiated | Pass |  |  |
| TC-06 | Borrow Record Lookup | Empty list | Empty list | Pass |  |  |
| TC-07 | Borrow Record Lookup | Not allowed to view other members' borrow records. | Display record BR003 of member Hoàng Cá Biệt | Fail | [BUG-07](bug-evidence/vkhanh-bug-07.png) | BUG-07 |
| TC-08 | Borrow Record Lookup | Display records BR002, BR005 with full details | Display records BR002, BR005 with full details | Pass | | |
| TC-09 | Borrow Record Lookup | Display record BR003 with full information. | Display record BR003 with full information. Status: "Quá hạn" | Pass |  |  |

---

## Test Summary

| Metric | Value |
|--------|---------|
| Total Test Cases | 48 |
| Pass | 36 |
| Fail | 11 |
| Blocked | 1 |
| Not Run | 0 |
| Pass Rate | 75% |

### Results by Functional Group

| Group | Total TCs | Pass | Fail | Blocked | Pass Rate |
|-------|-----------|------|------|---------|-----------|
| Login                 | 6 | 6 | 0 | 0 | 100%   |
| View Book List        | 2 | 2 | 0 | 0 | 100%   |
| Search & Filter Books | 6 | 5 | 1 | 0 | 83.33% |
| Borrow Book           | 7 | 5 | 2 | 0 | 71.43% |
| Return Book           | 4 | 2 | 2 | 0 | 50%    |
| Overdue Handling      | 4 | 4 | 0 | 0 | 100%   |
| Member Management     |10 | 5 | 4 | 1 | 50%    |
| Borrow Record Lookup  | 9 | 8 | 1 | 0 | 88.89% |

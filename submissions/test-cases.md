# Test Cases 

| Information | |
|---|---|
| **Group** | GROUP 8 |
| **Created Date** | 20/05/2026 |
| **System** | https://stqa.rbc.vn |
| **Reference** | SRS v1.0 |

---

## Step 1: Input Domain Modeling (IDM)

### IDM — Login (REQ-01)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Is the email valid? | Valid | `librarian@library.com` | Login successful |
| | Invalid | `nobody@test.com` | Msg: "Không tìm thấy thành viên" |
| Is the password valid? | Valid | `admin123` | Accepted |
| | Invalid | `wrongpass` | Msg: "Mật khẩu không đúng" |
| Is the input field empty? | Non-empty | (any value) | Normal processing  |
| | Empty | `" "` | Msg: "Vui lòng nhập..." |


### IDM — View Book List (REQ-02)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Who can view the book list? | Librarian | `LIB001` (Librarian) | Display complete book list |
|  | Member | `MEM002` (Member) | Display complete book list |
| Book Status? | Available | `BOOK018` | Display status as “**Có sẵn**” |
|  | Borrowed | `BOOK003` | Display status as “**Đang mượn**” |
|  | Lost | `BOOK020` | Display status as "**Thất lạc**" |
| Display Book info? | Name | `BOOK008` | Mạng máy tính |
| | Author | `BOOK008` | Lý Văn Tài |
| | Genre | `BOOK008` | Công nghệ |
| | Publish year | `BOOK008` | 2022 |
| Is there a real-time status update event? | Borrow event | Msg: "Book borrowed successfully!" | Status changes to "**Borrowed**" |
|  | Return event | Msg: "Book returned successfully!" | Status changes to "**Available**" |


### IDM — Search & Filter Books (REQ-03)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Does the keyword exist in the database? | Yes (book title) | `Flutter` | Display books containing "**Flutter**" |
| | Yes (author name) | `Nguyễn` | Display books written by authors containing "**Nguyễn**" |
| | No | `XYZ123` | Display "Không tìm thấy sách nào." |
| Is the search case-sensitive? | Lowercase | `flutter` | Same result as "**Flutter**" |
| | Uppercase | `FLUTTER` | Same result as "**Flutter**" |
| Does the category exist in the database? | Yes | `Kinh tế` | Display books in category "**Kinh tế**" (BOOK007, BOOK014, BOOK015) | 
| | No | `ABC` |  Display "Không tìm thấy sách nào." | 


### IDM — Borrow Book (REQ-04)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Book status? | Available | `BOOK001` | Allow borrowing |
| | Borrowed | `BOOK003` | Not allow borrowing |
| | Lost | `BOOK007` | Not allow borrowing |
| Member status? | Active | `MEM002` | Allow borrowing |
| | Suspended | `MEM004` | Reject, display error |
| | Expired | `MEM005` | Reject, display error |
| Number of borrowing books? | < 3 (BVA: 0, 1, 2) | `MEM006` (0 books) | Allow borrowing |
| | = 3 (BVA: limit) | `MEM` has borrowed 3 books | Reject, notify member has reached the limit |
| Due date? | 14 days after borrow date | Borrow date: **24/05/2026** | Due date: **07/06/2026** |

#### Decision Table for Borrow Book

| | | Rule 1 | Rule 2| Rule 3 | Rule 4 | Rule 5 |
|-------|---------|-------|---------|-----------|-----------|--------|
| Conditions | Suspended? | Yes | No | No | No | No |
| | Expired? | - | Yes | No | No | No |
| | Book available? | - | - | No | Yes | Yes |
| | At borrow limit? | - | - | - | Yes | No |
| Actions | Allow borrowing | | | | | X |
| | Refuse: book borrowed | | | X | | |
| | Refuse: limit reached | | | | X | | 
| | Refuse: suspended | X | | | | |
| | Refuse: expired | | X | | | |
| | Set due date to 14 days later | | | | | X |


### IDM — Return Book (REQ-05)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Current record status | Borrowing | `BR001` | - "**Trả sách**" button available <br> - Book status: "**Đang mượn**"|
| | Returned | `BR004` | - "**Trả sách**" button unavailable <br> - Book status: "**Có sẵn**" |
| Return date status | Return on time | N/A | Successfully returned the book. <br> - Record status: "**Đã trả**" <br> - Book status: "**Có sẵn**" <br> - Msg: "**Trả sách thành công.**" |  
| | Return late | `BR001` | Successfully returned the book. <br> - Record status: "**Đã trả**" <br> - Book status: "**Có sẵn**" <br> - Warning message: "**Trả sách quá hạn!**" (assumed wording) | 


### IDM — Overdue Handling (REQ-06)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Librarian checking record status | Overdue, not checked by librarian | `BR001` | Status: "**Đang mượn**" (DB remain unchanged) |
| | Overdue, checked by librarian | `BR001` (dueDate ≤ currentDate) | Status update to "**Quá hạn**" |
| | On-time, checked by librarian | N/A (dueDate > currentDate) | Status remained "**Đang mượn**" |
| | Returned, checked by librarian | `BR002` | Status remained "**Đã trả**" |
| List view permission | Librarian | Check `BR001`, `BR003`, `BR005` | Able to check all the overdue records |
| | Member |`MEM002` check `BR001`| Able to check their overdue record |


### IDM — Member Management (REQ-07)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Is the full name valid? | Non-empty | `Nguyễn Học Bá` | Accepted |
| | Empty | `" "` | Msg: "Họ tên không được để trống." | 
| Is the email valid? | Has  @ and dot (.) in domain | `user@domain.com` | Accepted |  
| | Missing @ in domain | `userdomain.com` | Msg: "Email không hợp lệ." |
| | Missing dot (.) in domain | `user@domain` | Msg: "Email không hợp lệ." |
| | Duplicate email | `cu.le@email.com`| Msg: "Email đã tồn tại." |
| | Empty | `" "` | Msg: "Email không được để trống." |
| Is the phone number valid?| Valid | `0923456789` | Accepted | 
| | Empty | `" "` | Msg: "Số điện thoại không được để trống." |


### IDM — Borrow Record Lookup (REQ-08)

| Characteristic | Block | Value | Expected Result |
|---|---|---|---|
| Search ID existence | Valid | `MEM002` | Display borrow records with full details: **Record ID**, **Book Title**, **Borrow Date**, **Due Date**, **Status**. |
| | Wrong casing | `mem002` | Msg: "No borrow records found." |
| | Leading/trailing spaces | `"MEM002"` | Msg: "No borrow records found." |
| | Invalid | `ABC123` / `!@#` | Msg: "No borrow records found." |
| | Empty | `" "` | No action initiated |
| View permission | Librarian | - Account: `librarian` <br> - Lookup: `MEM001` | Display borrow records with full details.|
| | Member - Lookup personal records | - Account: `ba.nguyen` <br> - Lookup: `MEM002` | Display borrow records with full details. |
| | Member - Lookup others' records | - Account: `ba.nguyen` <br> - Lookup: `MEM006` (of another member) | Empty list |
| Borrow status | Borrowing | `BR003` | Display full details with Status: "**Borrowing**". |
| | Returned | `BR002` | Display full details with Status: "**Returned**". |
| | Overdue | `BR001` | Display full details with Status: "**Overdue**". |
|Record per member | Multiple records | `MEM003` | Display all records `BR002`, `BR005`, each containing full details. |
| | Single record | `MEM006` | Display only 1 record `BR003` with full details. |
| | Zero record | `MEM004` | Empty list |

---

## Step 2: Test Cases

### REQ-01 — Login

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-----------------|---------------|-------------|-------------|------------------|-----|-----------|
| TC-01 | Login successful | User account exists in system. App is on Login page. | 1. Enter a valid email. <br> 2. Enter the correct password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `librarian@library.com` <br> Password: `admin123` | Login successful. Show username and role on the AppBar. | REQ-01 | EP |
| TC-02 | Login with **invalid email** (unregistered) | App is on Login page. | 1. Enter unregistered email. <br> 2. Enter any password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `nobody@test.com` <br> Password: `password123` | Msg: "Không tìm thấy thành viên." | REQ-01 | EP |
| TC-03 | Login with **valid email** but **wrong password**  | User account exists. App is on Login page. | 1. Enter registered email. <br> 2. Enter wrong password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `ba.nguyen@email.com` <br> Password: `wrongpassword` | Msg: "Mật khẩu không đúng." | REQ-01 | EP |
| TC-04 | Login with both **fields empty** | App is on Login page. | 1. Leave both fields blank. <br> 2. Click "Đăng nhập" button/Press "Enter". | Email: `" "` <br> Password: `" "` | Msg: "Vui lòng nhập email và mật khẩu." | REQ-01 | EP |
| TC-05 | Login with **email empty** but **password filled** | App is on Login page. | 1. Leave email blank. <br> 2. Enter any password. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `" "` <br> Password: `admin123` | Msg: "Vui lòng nhập email và mật khẩu." | REQ-01 | EP |
| TC-06 | Login with **email filled, password empty** | App is on Login page. | 1. Enter valid email.<br> 2. Leave password blank. <br> 3. Click "Đăng nhập" button/Press "Enter". | Email: `librarian@library.com` <br> Password: `" "` | Msg: "Vui lòng nhập email và mật khẩu." | REQ-01 | EP |


### REQ-02 — View Book List

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-----------------|---------------|-------------|-------------|------------------|-----|-----------|
| TC-01 | Verify that a **librarian** can view the **complete book list** | Login successful on librarian account | Open the Book List page | Account: `librarian@library.com` | Display all 20 books | REQ-02 | EP |
| TC-02 | Verify that a **member** can view the **complete book list** | Login successful on member account | Open the Book List page | Account: `dam.tran@email.com` | Display all 20 books | REQ-02 | EP |
| TC-03 | Verify that a **borrowed** book displays the **correct status** | Login successful with any valid account (Librarian or Member) | 1. Open the Book List page. <br> 2. Find borrowed book ID  | Book ID: `BOOK003` - Kiểm thử phần mềm nhập môn | Display status as “**Đang mượn**” | REQ-02 | EP |
| TC-04 | Verify that an **available book** displays the **correct status** | Login successful with any valid account (Librarian or Member) | 1. Open the Book List page. <br> 2. Find available book ID | Book ID: `BOOK001` - Lập trình Flutter cơ bản | Display status as “**Có sẵn**” | REQ-02 | EP |
| TC-05 | Verify that **lost books** are displayed **correctly** | Login successful with any valid account (Librarian or Member) | 1. Open the Book List page. <br> 2. Find lost book ID | Book ID: `BOOK007` - Kinh tế vi mô | Display status as “**Thất lạc**” | REQ-02 | EP |
| TC-06 | Verify that **book information** is displayed **correctly** | Login successful with any valid account (Librarian or Member) | 1. Open the Book List page. <br> 2. Find book ID | Book ID: `BOOK010` | Display correct: <br> - **Title**: An toàn thông tin cơ bản <br> - **Author**: Trần Quốc An <br> - **Category**: Công nghệ <br>- **Publication year**: 2023 <br> - **Status**: Có sẵn | REQ-02 | EP |
| TC-07 | Verify real-time status update **after borrowing** a book | Login with any valid account. <br> `BOOK001` was just borrowed (system displayed success message). | Open the **Sách** tab and locate `BOOK001`. | Borrow Event on `BOOK001` | Book status is updated immediately from “**Có sẵn**” to “**Đang mượn**” | REQ-02 | EP |
| TC-08 | Verify real-time status update **after returning** a book | Login as `ba.nguyen@email.com`. <br> `BR001` / `BOOK003` was just returned (system displayed success message). | Open the **Sách** tab and locate `BOOK003`. | Return Event on `BOOK003` | Book status is updated immediately from “**Đang mượn**” to “**Có sẵn**” | REQ-02 | EP |


### REQ-03 — Search & Filter Books

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-----------------|---------------|-------------|-------------|------------------|-----|-----------|
| TC-01 | Verify searching books by **title** | Login successful with any valid account (Librarian or Member) | 1. Open Book List page.<br>2. Enter keyword into search box. | Keyword: `Flutter` | Display `BOOK001` - Lập trình Flutter cơ bản | REQ-03 | EP |
| TC-02 | Verify searching books by **author** | Login successful with any valid account (Librarian or Member) | 1. Open Book List page.<br>2. Enter keyword into search box. | Keyword: `Nguyễn` | Display books by authors containing **Nguyễn** (BOOK001, BOOK006, BOOK009, BOOK016) | REQ-03 | EP |
| TC-03 | Verify search is **case-insensitive** | Login successful with any valid account (Librarian or Member) | 1. Open Book List page.<br>2. Enter keyword into search box. | Keyword: `flutter`/`FLUTTER` | Display `BOOK001` - Lập trình Flutter cơ bản | REQ-03 | EP |
| TC-04 | Verify system handles **non-existing keyword** | Login successful with any valid account (Librarian or Member) | 1. Open Book List page.<br>2. Enter keyword into search box. | Keyword: `XYZ123` | Display "Không tìm thấy sách nào." | REQ-03 | EP |
| TC-05 | Verify filtering books by **category** | Login successful with any valid account (Librarian or Member) | 1. Open Book List page.<br>2. Enter category into filter box. | Category: `Kinh tế` | Display only books in category **Kinh tế** (BOOK007, BOOK014, BOOK015) | REQ-03 | EP |
| TC-06 | Verify category filter is **case-insensitive** | Login successful with any valid account (Librarian or Member) | 1. Open Book List page.<br>2. Enter category into filter box. | Category: `kinh tế` / `KINH TẾ` | Returns the same result as **Kinh tế** (BOOK007, BOOK014, BOOK015) | REQ-03 | EP | 


### REQ-04 — Borrow Book

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-----------------|---------------|-------------|-------------|------------------|-----|-----------|
| TC-01 | Testing borrowing available book **successfully** on an **active** account at the borrow count of **1**| Login successfully on active account that has 1 book borrowed. | 1. Click on the **Mượn sách này** symbol on the book **Lập trình Flutter cơ bản**. <br>2. Confirm borrowing book. | Active account: `ba.nguyen@email.com`.<br> Available book: `Lập trình Flutter cơ bản `| - Confirm msg: **Mượn sách thành công!**<br> - A borrow card for **Lập trình Flutter cơ bản** appear in **Mượn / Trả** tab. <br> - Book status become **Đang mượn**. | REQ-04 | EP |
| TC-02 | Testing borrowing available book on an **active** account at the borrow count of **3** | Login successfully on active account that has 1 book borrowed. | 1. Borrow 2 available books **Lập trình Flutter cơ bản** and **Cấu trúc dữ liệu và giải thuật**  <br>2. Click on the **Mượn sách này** symbol on the book **Trí tuệ nhân tạo đại cương**. <br>3. Confirm borrowing book. | Active account: `ba.nguyen@email.com`.<br> Available book: <br> - Trí tuệ nhân tạo đại cương<br> - Cấu trúc dữ liệu và giải thuật<br> - Lập trình Flutter cơ bản | Error returned stating a member can only borrow up to 3 books. <br> - The book stays available <br> - The borrow book count remains unchanged. | REQ-04 | BVA |
| TC-03 | Testing borrowing available book on **suspended** account | Login successfully on suspended account | 1. Click on the **Mượn sách này** symbol on the book **Lập trình Flutter cơ bản**. <br>2. Confirm borrowing book. | Suspended account: `cu.le@email.com`.<br> Available book: `Lập trình Flutter cơ bản` | Error msg: "**Thành viên đã tạm ngưng. Không thể mượn sách.**". <br> - The book stays available. <br> - The borrow book count remains unchanged. | REQ-04 | EP |
| TC-04 | Testing borrowing available book on **expired** account | Login successfully on expired account | 1. Click on the **Mượn sách này** symbol on the book **Lập trình Flutter cơ bản**. <br>2. Confirm borrowing book. | Expired account: `binh.pham@email.com`.<br> Available book: `Lập trình Flutter cơ bản` | Error msg: "**Thành viên đã hết hạn. Không thể mượn sách.**". <br> - The book stays available. <br> - The borrow book count remains unchanged. | REQ-04 | EP |
| TC-05 | Testing to check the **14 days limit** of borrowing book | Login successfully on active account | 1. Click on the **Mượn sách này** symbol on the book **Lập trình Flutter cơ bản**. <br>2. Confirm borrowing book. | Active account: `ba.nguyen@email.com`.<br> Available book: `Lập trình Flutter cơ bản`.<br> Borrow date: `22/05/2026` | Due date of the borrow book is **05/06/2026** (14 days after **22/05/2026**) | REQ-04 | EP | 
| TC-06 | Testing borrowing borrowed book on an **active** account | Login successfully on active account | 1. Open **Sách** page. <br> 2. Locate the book. <br> 3. Observe UI. | Active account: `ba.nguyen@email.com`.<br> Borrowed book: `Quản trị nhân sự hiện đại` | Borrowed book does not have the **Mượn sách này** button | REQ-04 | EP 
| TC-07 | Testing borrowing **lost book** on an **active** account | Login successfully on active account | 1. Open **Sách** page. <br> 2. Locate the book. <br> 3. Observe UI. | Active account: `ba.nguyen@email.com`.<br> Lost book: `Kinh tế vi mô` | Lost book does not have the **Mượn sách này** button | REQ-04 | EP |


### REQ-05 — Return Book

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-----------------|---------------|-------------|-------------|------------------|-----|-----------|
| TC-01 | Display "**Trả sách**" button at borrow record | Login successfully on active account that has book borrowed and returned. | Go to "**Mượn / Trả**" tab. | Account: `ba.nguyen@email.com`.<br> - Borrowing record ID: `BR001`<br> - Returned record ID: `BR004` | "**Trả sách**" button available at record `BR001`, unavailable at `BR004`. | REQ 05 | EP |
| TC-02 | Return **overdue** book | Login successfully on active account that has 1 book borrowed overdue. | 1. Go to "**Mượn / Trả**” tab. <br> 2. Click "**Trả sách**" at borrow record. | Account: `ba.nguyen@email.com`.<br> Record ID: `BR001` | Record status: "**Đã trả**" + Update book status to "**Có sẵn**" + Warning message: "**Trả sách quá hạn!**" (assumed wording) | REQ 05 | EP |
| TC-03 | Return book **on time** | Login successfully on active account. <br> Borrow `BOOK006` to create a new record with dueDate > currentDate. | 1. Go to “**Mượn / Trả**” tab. <br> 2. Click "**Trả sách**" at borrow record. | Account: `dam.tran@email.com` <br> Record ID: `BR006` (dam.tran borrows BOOK006) | Record status: "**Đã trả**" + Update book status to "**Có sẵn**" + Msg: "**Trả sách thành công**" | REQ 05 | EP |


### REQ-06 — Overdue Handling

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-----------------|---------------|-------------|-------------|------------------|-----|-----------|
| TC-01 | Overdue book - **Not checked** by librarian | Login successful as librarian | Go to “**Mượn / Trả**” tab | - Account: `librarian@library.com` <br> - Record ID: `BR001` (dueDate ≤ currentDate) | Status of record `BR001`: "**Đang mượn**" (DB unupdated) | REQ-06 | EP |
| TC-02 | **Librarian check** overdue books | Login successful as librarian. <br> Borrow `BOOK006` to create a new record with dueDate > currentDate. | 1. Go to “**Mượn / Trả**” tab. <br> 2. Click “**Kiểm tra sách quá hạn**”. | - Account: `librarian@library.com` <br> - Records ID: `BR001` (dueDate ≤ currentDate), `BR002`, `BR006` (record of `BOOK006`)  | - Status of `BR001`: **Quá hạn** <br> - Status of `BR002`: **Đã trả** <br> - Status of `BR006`: **Đang mượn** | REQ-06 | EP |
| TC-03 | **Librarian** views **all** overdue borrow records. | Login successful as librarian, overdue books are checked | Go to “**Mượn / Trả**” tab | Account: `librarian@library.com` | Display records `BR001`, `BR003` with "**Quá hạn**" status | REQ 06 | EP |
| TC-04 | **Member** views **personal** overdue borrow records. | Login successful as member has borrow record, overdue books are checked | Go to “**Mượn / Trả**” tab | - Account: `ba.nguyen@email.com` <br> - Records: `BR001`, `BR004` | Display record `BR001` with "**Quá hạn**" status | REQ 06 | EP | 


### REQ-07 — Member Management

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|-------|-----------------|---------------|-------------|-------------|------------------|-----|-----------|
| TC-01 | Add member with **all valid inputs** | Logged in as Librarian. Add Member page is open. Email does not already exist. | 1. Enter valid full name. <br> 2. Enter valid email. <br> 3. Enter valid phone number.<br> 4. Click "**Thêm thành viên**" button.| Full name: `Nguyễn Linh Tinh` (non-empty) <br> Email: `linh.ng@email.com` (contains @, dot in domain) <br> Phone number: `0987654321` (exactly 10 digits, starts with 0) | New member created successfully. Member appears in member list. Member status: **Active** | REQ-07 | EP |
| TC-02 | Add member with invalid email — **missing @ in domain** | Logged in as Librarian. Add Member page is open. | 1. Enter valid full name. <br> 2. Enter email without @. <br> 3. Enter valid phone number. <br> 4. Click "**Thêm thành viên**" button. | Full name: `Nguyễn Linh Tinh` <br> Email: `linh.ngemail.com` <br> Phone number: `0987654321` | Msg: "Email không hợp lệ." | REQ-07 | EP |
| TC-03 | Add member with invalid email — **missing dot in domain** | Logged in as Librarian. Add Member page is open. | 1. Enter valid full name. <br> 2. Enter email missing dot. <br> 3. Enter valid phone number. <br> 4. Click "**Thêm thành viên**" button. | Full name: `Nguyễn Linh Tinh` <br> Email: `linhng@email` <br> Phone number: `0987654321` | Msg: "Email không hợp lệ." | REQ-07 | EP |
| TC-04 | Add member with **duplicate email** | Logged in as Librarian. Email already exists in system. Add Member page is open. | 1. Enter valid full name. <br> 2. Enter an email that already exists. <br> 3. Enter valid phone number. <br> 4. Click "**Thêm thành viên**" button. | Full name: `Nguyễn Biết Tuốt` <br> Email: `biet.hoang@email.com` <br> Phone number: `0918273645` | Msg: "Email đã tồn tại." | REQ-07 | EP |
| TC-05 | Add member with **empty email** | Logged in as Librarian. Add Member page is open. | 1. Enter valid full name. <br> 2. Leave email blank. <br> 3. Enter valid phone number. <br> 4. Click "**Thêm thành viên**" button. | Full name: `Nguyễn Linh Tinh` <br> Email: `" "` <br> Phone number: `0987654321` | Msg: "Email không được để trống." | REQ-07 | EP |
| TC-06 | Add member with **empty full name** | Logged in as Librarian. Add Member page is open. | 1. Leave full name blank. <br> 2. Enter valid email. <br> 3. Enter valid phone number. <br> 4. Click "**Thêm thành viên**" button. | Full name: `" "` <br> Email: `linh.ng@email.com` <br> Phone number: `0987654321` | Msg: "Họ tên không được để trống." | REQ-07 | EP |
| TC-07 | Add member with **empty phone number** | Logged in as Librarian. Add Member page open. | 1. Enter valid name. <br>  2. Enter valid email. <br> 3. Leave phone blank. <br> 4. Click "**Thêm thành viên**" button. | Full name: `Nguyễn Linh Tinh` <br> Email: `linh.ng@email.com` <br> Phone number: `" "` | Msg: "Số điện thoại không được để trống." | REQ-07 | EP |
| TC-08 | Add member with **all fields empty** | Logged in as Librarian. Add Member page is open. | 1. Leave all fields blank. <br> 2.Click "**Thêm thành viên**" button. | Full name: `" "` <br> Email: `" "` <br> Phone number: `" "` | Msg: "Họ tên không được để trống."  | REQ-07 | EP |
| TC-09 | Verify **Member** cannot add new member | Logged in as Member. |  | Account: `biet.hoang@email.com` | "**Thêm thành viên**" button not exist . | REQ-07 | EP |


### REQ-08 — Borrow Record Lookup

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

## Summary

| Function Group | Number of TCs | Covered REQs | Applied IDM Techniques |
|----------------|---------------|---------------|-------------------------|
| Login | 6 | REQ-01 | EP |
| View Book List | 8 | REQ-02| EP |
| Search & Filter Books | 6 | REQ-03| EP |
| Borrow Book | 7 | REQ-04 | EP, BVA, Decision Table |
| Return Book | 3 | REQ-05 | EP |
| Overdue Handling | 4 | REQ-06 | EP |
| Member Management | 9 | REQ-07 | EP |
| Borrow Record Lookup | 8 | REQ-08 | EP, BVA |
| **Total** | 51 | 8 | 3 |


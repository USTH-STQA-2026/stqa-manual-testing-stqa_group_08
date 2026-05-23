# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

### IDM — Borrow book (REQ-04)

| Characteristic | Block | Represent value | Expected result |
|---|---|---|---|
| Book status? | Available | BOOK001 | Allow borrowing |
| | Borrowed | BOOK003 | Not allow borrowing |
| | Thất lạc | BOOK007 | Not allow borrowing |
| Member status? | Active | MEM002 | Allow borrowing |
| | Suspended | MEM004 | Reject, display error |
| | Expired | MEM005 | Reject, display error |
| Number of borrowing books? | < 3 (BVA: 0, 1, 2) | MEM006 (0 books) | Allow borrowing |
| | = 3 (BVA: limit) | MEM has borrowed 3 books | Reject, notify member has reached the limit |

---

## Bước 2: Test Cases

<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| TC ID | Test objectives | Precondition | Test steps | Input value | Expected result | REQ | Technique |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Testing borrowing available book successfully on an active account at the borrow count of 1| Login successfully on active account **ba.nguyen@email.com** | 1. Click on the **Borrow this book** symbol on the book **Lập trình Flutter cơ bản**. 2. Confirm borrowing book. | Active account: **ba.nguyen@email.com**. Available book: **Lập trình Flutter cơ bản** | Confirm notification **Book borrowed successfully!**, a borrow card for **Lập trình Flutter cơ bản** appear in the **Borrow / Return**, the book state become **Borrowed** | REQ-04 | EP |
| TC-02 | Testing borrowing available book on an active account at the borrow count of 3 | Login successfully on active account **ba.nguyen@email.com** and have 3 books borrowed | 1. Click on the **Borrow this book** symbol on the book **Trí tuệ nhân tạo đại cương**. 2. Confirm borrowing book. | Active account: **ba.nguyen@email.com**. Available book: **Trí tuệ nhân tạo đại cương** | Error returned stating a member can only borrow up to 3 books, the book stays available, the borrow book count remains unchanged | REQ-04 | BVA |
| TC-03 | Testing borrowing available book successfully on an active account at the borrow count of 2 | Login successfully on active account **ba.nguyen@email.com** and have 2 books borrowed | 1. Click on the **Borrow this book** symbol on the book **Trí tuệ nhân tạo đại cương**. 2. Confirm borrowing book. | Active account: **ba.nguyen@email.com**. Available book: **Trí tuệ nhân tạo đại cương** | Confirm notification **Book borrowed successfully!**, a borrow card for **Trí tuệ nhân tạo đại cương** appear in the **Borrow / Return**, the book state become **Borrowed** | REQ-04 | BVA |
| TC-04 | Testing borrowing available book on suspended account **cu.le@email.com** | Login successfully on suspended account **cu.le@email.com** | 1. Click on the **Borrow this book** symbol on the book **Lập trình Flutter cơ bản**. 2. Confirm borrowing book. | Suspended account: **cu.le@email.com**. Available book: **Lập trình Flutter cơ bản** | Refused to borrow book for the account is suspended, the book stays available, the borrow book count remains unchanged | REQ-04 | EP |
| TC-05 | Testing borrowing available book on expired account **binh.pham@email.com** | Login successfully on expired account **binh.pham@email.com** | 1. Click on the **Borrow this book** symbol on the book **Lập trình Flutter cơ bản**. 2. Confirm borrowing book. | Expired account: **binh.pham@email.com**. Available book: **Lập trình Flutter cơ bản** | Refused to borrow book for the account is expired, the book stays available, the borrow book count remains unchanged | REQ-04 | EP |
| TC-06 | Testing to check the 14 days limit of borrowing book | Login successfully on active account **ba.nguyen@email.com** | 1. Click on the **Borrow this book** symbol on the book **Lập trình Flutter cơ bản**. 2. Confirm borrowing book. | Active account **ba.nguyen@email.com**. Available book: **Lập trình Flutter cơ bản**. Borrow date: 22/05/2026 | Due date of the borrow book is 05/06/2026 (14 days after 22/05/2026) | REQ-04 | EP |
| TC-07 | Testing borrowing borrowed book  on an active account | Login successfully on active account **ba.nguyen@email.com** | | Active account: **ba.nguyen@email.com**. Borrowed book: **Quản trị nhân sự hiện đại** | Borrowed book does not have the **Borrow this book** button | REQ-04 | EP |
| TC-08 | Testing borrowing lost book  on an active account | Login successfully on active account **ba.nguyen@email.com** | | Active account: **ba.nguyen@email.com**. Lost book: **Kinh tế vi mô** | Lost book does not have the **Borrow this book** button | REQ-04 | EP |

---

## Tổng hợp

| Functional groups | Number of TC | REQ covered | Applied IDM technique |
|----------------|-------|---------|----------------------|
| Borrow book | 8 | REQ-04 | EP, BVA |
| **Total** | 8 | 1 | 2 |

---

## Decision Table

| | | Rule 1 | Rule 2| Rule 3 | Rule 4 | Rule 5 |
|-------|---------|-------|---------|-----------|-----------|--------|
| Conditions | Book available? | Yes | No | Yes | Yes | Yes |
| | At borrowing limit? | No | - | Yes | No | No |
| | Suspended? | No | - | - | Yes | No |
| | Expired? | No | - | - | - | Yes |
| Actions | Allow borrowing | X | | | | |
| | Refuse: book borrowed | | X | | | |
| | Refuse: limit reached | | | X | | | 
| | Refuse: suspended | | | | X | |
| | Refuse: expired | | | | | X |
| | Set due date to 14 days later | X | | | | |

---
# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

---

## Kết quả chi tiết

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| 01 | Borrow book | Book borrowed successfully on active account not at the borrow limit | Book borrowed successfully on active account not at the borrow limit | Pass | | |
| 02 | Borrow book | Fail to borrow book on active account at the borrow limit | Book borrow successfully | Fail | submission/image/kien-bug-01 | An active member can borrow the fourth book |
| 03 | Borrow book | Book borrowed successfully on active account near the borrow limit | Book borrowed successfully on active account not at the borrow limit | Pass | | |
| 04 | Borrow book | Fail to borrow book on suspended account with the reason of being suspended | Error notification state that member cannot borrow book for being expired | Fail | submission/image/kien-bug-02 | Suspended member be labeled as expired |
| 05 | Borrow book | Fail to borrow book on expired account with the reason of being expired | Error notification state that member cannot borrow book for being expired | Pass | | |
| 06 | Borrow book | Due date being 14 days after the borrow date | Due date being 14 days after the borrow date | Pass | | |
| 07 | Borrow book | Unable to borrow borrowed books | Unable to borrow borrowed books | Pass | | |
| 08 | Borrow book | Unable to borrow lost books | Unable to borrow lost books | Pass | | |
 
---

## Tổng hợp kết quả

| Statistic | Value |
|--------|---------|
| Number of test case | 8 |
| Pass | 6 |
| Fail | 2 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass rate** | 75% |

### Kết quả theo nhóm chức năng

| Functional groups | Total TC | Pass | Fail | Pass rate |
|------|---------|------|------|------------|
| Borrow book | 8 | 6 | 2 | 75% |

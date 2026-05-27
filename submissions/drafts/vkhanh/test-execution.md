# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Borrow Record Lookup | Display record `BR002`, `BR005` with full information. | Display record `BR002`, `BR005` with full information. | Pass |  |  |
| TC-02 | Borrow Record Lookup | Msg: "No borrow records found." | Msg: "No borrow records found." | Pass |  |  |
| TC-03 | Borrow Record Lookup | Msg: "No borrow records found." | Msg: "No borrow records found." | Pass |  |  |
| TC-04 | Borrow Record Lookup | Msg: "No borrow records found." | Msg: "No borrow records found." | Pass |  |  |
| TC-05 | Borrow Record Lookup | No action initiated | No action initiated | Pass |  |  |
| TC-06 | Borrow Record Lookup | Display record `BR003` with full information. | Display record `BR003` with full information. | Pass |  |  |
| TC-07 | Borrow Record Lookup | Empty list | Empty list | Pass |  |  |
| TC-08 | Borrow Record Lookup | Not allowed to view other members' borrow records. | Display record `BR003` of member Hoàng Cá Biệt | Fail | vkhanh-bug-01 | BUG-01 |
| TC-09 | Borrow Record Lookup | Record `BR001` status is `Overdue` | Status is `Overdue` | Pass |  |  |


---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 9 |
| Pass | 8 |
| Fail | 1 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 88.89% |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |

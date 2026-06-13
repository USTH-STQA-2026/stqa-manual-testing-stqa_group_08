# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

---

## Kết quả chi tiết

| TC ID | Functional groups | Expected result (summary) | Actual result | Conclusion | Prove | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Borrow Record Lookup | Display record `BR002`, `BR005` with full information. | Display record `BR002`, `BR005` with full information. | Pass |  |  |
| TC-02 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-03 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-04 | Borrow Record Lookup | Msg: "Không tìm thấy phiếu mượn." | Msg: "Không tìm thấy phiếu mượn." | Pass |  |  |
| TC-05 | Borrow Record Lookup | No action initiated | No action initiated | Pass |  |  |
| TC-06 | Borrow Record Lookup | Empty list | Empty list | Pass |  |  |
| TC-07 | Borrow Record Lookup | Not allowed to view other members' borrow records. | Display record `BR003` of member Hoàng Cá Biệt | Fail | [BUG-07](.../bug-evidence/vkhanh-bug-07.png) | BUG-07 |
| TC-08 | Borrow Record Lookup | Display record `BR003` with full information. | Display record `BR003` with full information. Status is `Quá hạn` | Pass |  |  |

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

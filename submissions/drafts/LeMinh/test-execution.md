# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-REQ02-01 | View Book List | Display all 20 books for librarian account | System displayed all 20 books correctly | Pass | | |
| TC-REQ02-02 | View Book List | Display all 20 books for member account | System displayed all 20 books correctly | Pass | | |
| TC-REQ02-03 | View Book List | Display status as “Đang mượn” | BOOK003 displayed status “Đang mượn” correctly | Pass | | |
| TC-REQ02-04 | View Book List | Display status as “Có sẵn” | BOOK001 displayed status “Có sẵn” correctly | Pass | | |
| TC-REQ02-05 | View Book List | Display status as “Thất lạc” | BOOK007 displayed status “Thất lạc” correctly | Pass | | |
| TC-REQ02-06 | View Book List | Display correct book information | BOOK010 information displayed correctly | Pass | | |
| TC-REQ02-07 | View Book List | Status updates to “Đang mượn” immediately | Status updated immediately | Pass | | |
| TC-REQ02-08 | View Book List | Status updates to “Có sẵn” immediately | Status updated immediately | Pass | | |
| TC-REQ03-01 | Search & Filter Books | Display BOOK001 when searching “Flutter” | Search returned BOOK001 correctly | Pass | | |
| TC-REQ03-02 | Search & Filter Books | Display books by authors containing “Nguyễn” | System returned BOOK001, BOOK006, BOOK009, BOOK016 | Pass | | |
| TC-REQ03-03 | Search & Filter Books | Lowercase and uppercase search return same result | “flutter” and “FLUTTER” returned the same result as “Flutter” | Pass | | |
| TC-REQ03-04 | Search & Filter Books | Display “Không tìm thấy sách nào.” | System displayed “Không tìm thấy sách nào.” correctly | Pass | | |
| TC-REQ03-05 | Search & Filter Books | Display only books in category “Kinh tế” | System displayed BOOK007, BOOK014, BOOK015 correctly | Pass | | |
| TC-REQ03-06 | Search & Filter Books | Category filter is case-insensitive | “kinh tế” and “KINH TẾ” returned different results from "Kinh tế" | Fail | submission/image/leminh-bug-01 | BUG-01 |
---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `<!-- số -->` |
| Pass | `<!-- số -->` |
| Fail | `<!-- số -->` |
| Blocked | `<!-- số -->` |
| Not Run | `<!-- số -->` |
| **Tỷ lệ Pass** | `<!-- xx% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |

# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|----------------|----------------------------|--------------|----------|------------|-----|
| TC-01 | Login | Login successful | Login successful | Pass | | | 
| TC-02 | Login | Msg: "Không tìm thấy thành viên." | Msg: "Không tìm thấy thành viên." | Pass | | |
| TC-03 | Login | Msg: "Mật khẩu không đúng." |  Msg: "Mật khẩu không đúng." | Pass | | |
| TC-04 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |
| TC-05 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |
| TC-06 | Login | Msg: "Vui lòng nhập email và mật khẩu." | Msg: "Vui lòng nhập email và mật khẩu." | Pass | | |
| TC-07 | Login | Msg: "Không tìm thấy thành viên." | Msg: "Không tìm thấy thành viên." | Pass | | |
| TC-08 | Member Management | New member created successfully. | Msg: "Email không hợp lệ" | Fail | `blinh-BUG-01-TC-08` | 01 |
| TC-09 | Member Management | Msg: "Email không hợp lệ." | Msg: "Email không hợp lệ." | Pass | | |
| TC-10 | Member Management | Msg: "Email không hợp lệ." | New member created successfully. | Fail | `blinh-BUG-01-TC-10-1`, `blinh-BUG-01-TC-10-2` | 01 |
| TC-11 | Member Management | Msg: "Email đã tồn tại." | System triggers format error before duplicate check: "Email không hợp lệ." | Fail | `blinh-BUG-02` | 02 |
| TC-12 | Member Management | Msg: "Họ tên không được để trống." | Msg: "Họ tên không được để trống." | Pass | | |
| TC-13 | Member Management | Msg: "Email không được để trống." | Msg: "Email không hợp lệ." | Fail | `blinh-BUG-01-TC-13` | 01 |
| TC-14 | Member Management | Show "Required" error message. | Msg: "Họ tên không được để trống." (Successfully blocked) | Pass | | |
| TC-15 | Member Management | "Thêm thành viên" button does not exist. | "Thêm thành viên" button does not exist. | Pass | | |
| TC-16 | Member Management | Msg: "Số điện thoại không hợp lệ." | Msg: "Email không hợp lệ." | Blocked | | |
| TC-17 | Member Management | Msg: "Số điện thoại không hợp lệ." | Msg: "Email không hợp lệ." | Blocked | | |
| TC-18 | Member Management | Msg: "Số điện thoại không hợp lệ." | Msg: "Email không hợp lệ." | Blocked | | |
| TC-19 | Member Management | Msg: "Số điện thoại không hợp lệ." | Msg: "Email không hợp lệ." | Blocked | | |
| TC-20 | Member Management | Msg: "Số điện thoại không hợp lệ." | Msg: "Email không hợp lệ." | Blocked | | |

---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `20` |
| Pass | `11` |
| Fail | `4` |
| Blocked | `5` |
| Not Run | `0` |
| **Tỷ lệ Pass** | `55%` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Login | `7` |`7`|`0`|`100%`|
| Member Management | `13` |`4`|`4`|`30.77%`|


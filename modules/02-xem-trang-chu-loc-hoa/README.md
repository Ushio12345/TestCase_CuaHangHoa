# 02 – Xem trang chủ & lọc hoa (`/`, `/hoa`)

[← Về trang chính](../../README.md)

## Mô tả chức năng

Người dùng xem trang chủ và danh sách hoa theo loại hoa: chọn một loại ở thanh Danh mục bên trái, hệ thống hiển thị lưới các hoa đang hiển thị (`trang_thai = 1`) thuộc loại đó, kèm giá định dạng tiền Việt Nam. (SRS – Xem trang chủ và lọc hoa)

| Sheet | Chức năng con | URL | Trạng thái |
|---|---|---|---|
| 02.1 Trang chủ | Trang chủ | `/` | ✅ Test Design + Test Case (38 TC), chưa thực thi |
| 02.2 Danh sách & lọc hoa | Danh sách hoa, lọc theo loại | `/hoa`, `/hoa?loai=N` | ✅ Test Design + Test Case (69 TC), chưa thực thi |

- **Tác nhân:** Khách vãng lai, Thành viên, Quản trị viên
- **Chức năng liên quan:** Tìm kiếm sản phẩm, Chi tiết sản phẩm & thêm vào giỏ, Quản lý loại hoa, Quản lý sản phẩm hoa

## Quy tắc nghiệp vụ chính (đã confirm)

| Quy tắc | Giá trị |
|---|---|
| Hoa được hiển thị | Chỉ `trang_thai = 1`; hoa Ẩn / đã xóa (xóa mềm) không hiện (SRS bước 3; qa-log 12 #45, #74) |
| Loại hoa chưa có sản phẩm | FC_36 "Chưa có sản phẩm nào thuộc loại này" |
| Định dạng giá | `150.000đ` (SRS – Định dạng tiền tệ) |
| Phân trang `/hoa` | 8 sản phẩm / trang; URL có tham số trang; dạng `< 1 2 3 >`, trang 1 nút `<` disable, trang cuối nút `>` disable; 1 trang → hiện "1" (#4, #24, #29). Lỗi cố ý số 2: nút 1, 2, 3, Tiếp là phần tử tĩnh |
| Sắp xếp | Mới nhất (`ngay_d` mới nhất trước) · Giá tăng dần · Giá giảm dần; trùng ngày / cùng giá → tên A → Z; đổi loại / chuyển trang giữ kiểu đang chọn (#5, #20, #27) |
| Thẻ sản phẩm | Bấm ảnh / tên → `/hoa/[ma_hoa]`; tên dài cắt 1 dòng "…", hover → tooltip tên đầy đủ; nút thêm vào giỏ: chỉ kiểm tra badge giỏ hàng (#6, #7, #21) |
| Dòng đếm | N = tổng số hoa trong bộ lọc (#8) |
| Danh mục | Hiển thị tất cả loại hoa, tô sáng loại đang chọn, thứ tự thêm (loại mới ở cuối, `ma_loai` tăng dần); loại chưa có hoa → FC_36 (#9, #22, #28) |
| FC_36 | Thay lưới sản phẩm, ẩn dòng đếm và phân trang, vẫn hiện Sắp xếp (#11); `?loai=` không hợp lệ → FC_36 (#12); "Tất cả" khi không có hoa → FC_36 (#23) |
| Hoa không có loại (`ma_loai` NULL) | Hiển thị ở "Tất cả các loại hoa" (#13) |
| Ảnh lỗi / trống | Hiển thị alt = tên hoa, cả trang khách và trang quản lý (#14, #25) |
| Trang chủ – Thiết Kế Mới Nhất | 4 thẻ mới nhất (ngày tạo); nút "Xem toàn bộ sưu tập" → `/hoa` (#2, #17) |
| Trang chủ – Khám phá ngay | → `/hoa` (#18) |
| Trang chủ – Danh mục | Mặc định "Tất cả các loại hoa"; bấm loại hoa → `/hoa` (#3) |
| Trang chủ – Hoa đặc biệt | Danh sách **đang fix cứng** – không test lấy đúng danh sách; bấm → `/hoa/[ma_hoa]`; hoa Ẩn / đã xóa không hiển thị (#2, #19) |
| Khung bên phải | Chỉ test hiển thị: chưa đăng nhập → ô đăng nhập; đã đăng nhập → thông tin tài khoản. Quản trị viên mở trang khách → ô đăng nhập. Chức năng của khung và Tìm kiếm nhanh → module sau (#1, #15, #26, #30) |

Chi tiết câu hỏi và trả lời: [qa-log.md](qa-log.md) (#1 – #30 đã confirm).

## Tài liệu

| Tài liệu | File |
|---|---|
| Test Design (mindmap) | [test-design.md](test-design.md) |
| Test Case | [test-cases.xlsx](test-cases.xlsx) |

## Thống kê Test Case

File [test-cases.xlsx](test-cases.xlsx): mỗi chức năng con 1 sheet, ID có tiền tố riêng (`TCHU_` · `DSH_`); sheet `Tổng hợp` gom cả 2 sheet.

### 02.1 Trang chủ (`TCHU_01…TCHU_38`)

| Kịch bản chính | Số TC |
|---|---|
| FUNCTION – Hiển thị trang chủ và khối "Thiết Kế Mới Nhất" | 4 |
| FUNCTION – Điều hướng từ trang chủ | 6 |
| VALIDATION – Hiển thị giá và tên hoa trên thẻ ở trang chủ | 2 |
| UI – Giao diện mặc định | 4 |
| UI – Behavior | 9 |
| UI – Responsive | 2 |
| PHÂN QUYỀN – Xem trang chủ theo từng tác nhân | 4 |
| ẢNH HƯỞNG – Trang chủ cập nhật khi Quản trị viên thay đổi hoa và loại hoa | 7 |
| **Tổng** | **38** (HIGH 21 · MEDIUM 2 · LOW 15) |

### 02.2 Danh sách & lọc hoa (`DSH_01…DSH_69`)

| Kịch bản chính | Số TC |
|---|---|
| FUNCTION – Xem danh sách tất cả hoa | 5 |
| FUNCTION – Lọc danh sách hoa theo loại | 9 |
| FUNCTION – Sắp xếp danh sách hoa | 7 |
| FUNCTION – Phân trang danh sách hoa (8 hoa / trang) | 6 |
| FUNCTION – Thao tác trên thẻ sản phẩm | 2 |
| VALIDATION – Kiểm tra tham số loai không hợp lệ trên URL | 6 |
| VALIDATION – Hiển thị giá và tên hoa trên thẻ | 2 |
| UI – Giao diện mặc định | 6 |
| UI – Behavior | 9 |
| UI – Responsive | 2 |
| PHÂN QUYỀN – Xem và lọc danh sách hoa theo từng tác nhân | 4 |
| ẢNH HƯỞNG – Danh sách hoa cập nhật khi Quản trị viên thay đổi sản phẩm hoa | 8 |
| ẢNH HƯỞNG – Danh mục cập nhật khi Quản trị viên thay đổi loại hoa | 3 |
| **Tổng** | **69** (HIGH 44 · MEDIUM 8 · LOW 17) |

**Toàn module: 107 TC** (HIGH 65 · MEDIUM 10 · LOW 32). Form checklist (Function) không áp dụng: chức năng không có form nhập liệu. TC phân trang đối chiếu lỗi cố ý số 2 (dự kiến Failed).

## Kết quả thực thi

| Lần chạy | Ngày | Pass | Fail | Untested | Ghi chú |
|---|---|---|---|---|---|
| R1 | – | – | – | – | Chưa thực thi |

## Bug phát hiện

| Bug ID | Tiêu đề | Mức độ | TC liên quan |
|---|---|---|---|
| – | – | – | – |

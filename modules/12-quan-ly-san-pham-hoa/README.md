# 12 – Quản lý sản phẩm hoa (`/quan-tri/hoa`)

[← Về trang chính](../../README.md)

## Mô tả chức năng

Quản trị viên xem danh sách, thêm mới, sửa và xóa sản phẩm hoa.

| Sheet | Chức năng con | SRS | Trạng thái |
|---|---|---|---|
| 12.1 Danh sách hoa | Danh sách sản phẩm hoa (`/quan-tri/hoa`) | Không có mục chức năng (chỉ ảnh màn hình) | ✅ Test Design + Test Case (29 TC), chưa thực thi |
| 12.2 Thêm hoa | Thêm hoa mới (`/quan-tri/hoa/them`) | 4.3.4.1 | ✅ Test Design + Test Case (158 TC), chưa thực thi |
| 12.3 Sửa hoa | Sửa sản phẩm hoa (`/quan-tri/hoa/sua/[ma_hoa]`) | 4.3.4.2 | ✅ Test Design + Test Case (71 TC), chưa thực thi |
| 12.4 Xóa hoa | Xóa sản phẩm hoa | 4.3.4.3 | 🟡 Test Design + Test Case (24 TC); còn ❓ qa-log #76 (hoa đã xóa trùng trạng thái Ẩn) |

- **Tác nhân:** Quản trị viên (Khách vãng lai, Thành viên bị từ chối – lỗi 401)
- **Chức năng liên quan:** Quản lý loại hoa, Xem trang chủ & lọc hoa, Tìm kiếm, Chi tiết sản phẩm, Giỏ hàng, Thống kê tổng quan

## Quy tắc nghiệp vụ chính – Thêm hoa mới (đã confirm)

| Trường / Hành động | Quy tắc |
|---|---|
| Tên hoa | 5 – 20 ký tự (tính sau khi cắt khoảng trắng), chặn gõ quá 20; nhận chữ có dấu, chữ số và `.` `_` `;` `-` `,` `:` `(` `)` `/` `'`; ký tự đặc biệt khác → coi như trống (FC_16) hoặc "Tên hoa không hợp lệ"; không nhận emoji; cắt khoảng trắng đầu/cuối; cho phép trùng tên |
| Giá bán | Chỉ nhập được số (không `,` `.`), 5.000 – 7.000.000 (gồm 2 mốc); bỏ số 0 đứng đầu và khoảng trắng; không định dạng trong ô nhập |
| Mô tả | Tối đa 250 ký tự (tính cả xuống dòng), chặn gõ quá 250, có bộ đếm; nhận ký tự đặc biệt và emoji |
| Đường dẫn hình ảnh | Chỉ cần là link, tối đa 500 ký tự (SRS), quá 500 → "Đường dẫn ảnh vượt quá 500 ký tự"; không phải link → "Đường dẫn ảnh không hợp lệ"; trống / ảnh lỗi → hiển thị alt = tên hoa (cập nhật 19/11, qa-log 02 #25) |
| Nút Tải lên | Chỉ bấm được khi ô đường dẫn có nội dung; chỉ kiểm tra đường dẫn hợp lệ (chưa có upload file), tự điền đường dẫn, hỏi trước khi thay đường dẫn cũ |
| Để trống | Mã theo bảng trường: Tên hoa FC_16, Giá FC_20, Mô tả FC_23 (chỉ khoảng trắng cũng tính là trống) |
| Loại hoa, Trạng thái | Bắt buộc; Loại hoa mặc định là giá trị đầu tiên trong danh sách |
| Nút Làm lại | Xóa trắng ô nhập và thông báo lỗi; Loại hoa → "Hoa chia buồn"; Trạng thái → "Hiển thị" |
| Quay lại / tải lại trang / đóng tab khi đang nhập | Popup hỏi lưu thông tin |
| Thêm thành công | Chuyển về danh sách hoa, hoa mới hiển thị đầu tiên; thông báo tự ẩn sau 5 giây hoặc bấm tắt; bấm liên tục chỉ tạo 1 bản ghi |
| Phiên quản trị hết hạn | Chuyển về trang đăng nhập, mất dữ liệu đã nhập |
| Nút lưu | Tên theo màn hình: "Thêm mới" |
| Nhiều trường lỗi | Báo lỗi tất cả các trường |
| Texthint | Theo SRS |
| Ảnh hưởng | Hoa Ẩn không xuất hiện trong Tìm kiếm và danh sách hoa ở trang chủ; Thống kê đếm cả hoa Ẩn |

## Quy tắc nghiệp vụ chính – Sửa / Xóa / Danh sách (đã confirm)

| Hành động | Quy tắc |
|---|---|
| Sửa – màn hình | Trang riêng `/quan-tri/hoa/sua/[ma_hoa]`, đủ các trường như Thêm; mọi quy tắc của Thêm áp dụng cho Sửa |
| Sửa – nút | Nút lưu "Cập nhật thông tin"; Làm lại, Quay lại, Tải lên giống Thêm |
| Sửa thành công | Popup "Tuyệt vời!" – "Thông tin hoa đã được cập nhật thành công!", nút "ĐÓNG CỬA SỔ" → về danh sách; hoa giữ vị trí, `ngay_d` không đổi; không sửa gì vẫn ghi CSDL và hiện popup |
| Sửa – ngoại lệ | Hoa không tồn tại → "Không tìm thấy sản phẩm" (hoặc 404); hoa bị xóa khi đang sửa → báo lỗi, không tạo bản ghi mới |
| Sửa – ảnh hưởng | Giỏ hàng đổi giá ngay; đơn hàng cũ giữ `gia_ban` cũ |
| Xóa | Nút Xóa trên từng dòng; hộp thoại "Bạn có thực sự muốn xóa sản phẩm này không?" (Đồng ý xóa / Huỷ), Esc / bấm ra ngoài không đóng; thành công → "Đã xoá thành công"; xóa mềm: `trang_thai = 0`, không `DELETE` (hoa đã xóa vs hoa Ẩn: ❓ #76) |
| Xóa – ảnh hưởng | Hoa đã trong đơn hàng vẫn xóa được, hiển thị làm mờ trong đơn; trong giỏ → khi thanh toán yêu cầu xóa khỏi giỏ; `/hoa/[id]` → 404; Xóa loại hoa không tính hoa đã xóa; FC_26 tạm bỏ qua |
| Danh sách | Thuộc module 12 (SRS chỉ có ảnh màn hình); hiển thị cả hoa Ẩn (cột Trạng thái "Ẩn"); sắp xếp theo thời gian tạo (`ngay_d`), mới nhất lên đầu; 20 hoa / trang; giá dạng "450.000đ" |
| Danh sách – tìm kiếm, lọc | Tìm theo một phần tên, không phân biệt chữ hoa / thường và có dấu / không dấu; bấm "Áp dụng" hoặc Enter; ô trống → toàn bộ; không có kết quả → danh sách rỗng. Lọc: "Tất cả loại hoa" + các loại trong `loai_hoa`; tìm và lọc áp dụng cùng lúc |

Chi tiết câu hỏi và trả lời: [qa-log.md](qa-log.md) (76 câu: #1 – #75 ✅ · #76 ❓ – hoa đã xóa và hoa Ẩn cùng `trang_thai = 0`).

## Tài liệu

| Tài liệu | Xem online | File |
|---|---|---|
| Test Design (mindmap) | [test-design.md](test-design.md) | – |
| Test Case | Google Sheets: [12.1 Danh sách hoa](https://docs.google.com/spreadsheets/d/1KgZI0jVNESa4P1WYLJnznRT4CGR7Mzlww-tiGYN7k_E/edit?gid=1750116678#gid=1750116678) · [12.2 Thêm hoa](https://docs.google.com/spreadsheets/d/1KgZI0jVNESa4P1WYLJnznRT4CGR7Mzlww-tiGYN7k_E/edit?gid=1250044123#gid=1250044123) · [12.3 Sửa hoa](https://docs.google.com/spreadsheets/d/1KgZI0jVNESa4P1WYLJnznRT4CGR7Mzlww-tiGYN7k_E/edit?gid=1967646398#gid=1967646398) · [12.4 Xóa hoa](https://docs.google.com/spreadsheets/d/1KgZI0jVNESa4P1WYLJnznRT4CGR7Mzlww-tiGYN7k_E/edit?gid=1782277388#gid=1782277388) | [test-cases.xlsx](test-cases.xlsx) |

> Test Design 299 node lá (4 node `[Cần xác nhận BA/PO]`), Test Case 282 TC: Thêm 158 · Sửa 71 · Xóa 24 · Danh sách 29. Mọi node lá có ≥ 1 TC (trừ node ghi chú: "R + 1 O trùng", "Mô tả không có giá trị sai", "FC_26 tạm bỏ qua").

## Thống kê Test Case

File [test-cases.xlsx](test-cases.xlsx): mỗi chức năng con 1 sheet, ID có tiền tố riêng (`DS_` · `THEM_` · `SUA_` · `XOA_`); sheet `Tổng hợp` gom cả 4 sheet.

### 12.1 Danh sách hoa – Danh sách sản phẩm hoa (`DS_01…DS_29`)

| Kịch bản chính | Số TC |
|---|---|
| FUNCTION – Xem, tìm kiếm và lọc danh sách sản phẩm hoa | 14 |
| VALIDATION – Kiểm tra validate ô Tìm kiếm tên hoa | 2 |
| UI – Giao diện mặc định | 5 |
| UI – Behavior | 4 |
| UI – Responsive | 2 |
| PHÂN QUYỀN – Khách vãng lai và Thành viên bị chặn khi xem danh sách sản phẩm hoa | 2 |
| **Tổng** | **29** (HIGH 16 · MEDIUM 2 · LOW 11) |

### 12.2 Thêm hoa – Thêm hoa mới (`THEM_01…THEM_158`)

| Kịch bản chính | Số TC |
|---|---|
| FUNCTION – Thêm hoa mới thành công khi nhập dữ liệu hợp lệ | 11 |
| FUNCTION – Thêm hoa mới thất bại khi thiếu trường bắt buộc hoặc có trường không hợp lệ | 12 |
| FUNCTION – Kiểm tra đường dẫn ảnh bằng nút Tải lên | 6 |
| FUNCTION – Làm lại form Thêm hoa mới | 3 |
| FUNCTION – Điều hướng vào và ra màn hình Thêm hoa mới | 6 |
| VALIDATION – Kiểm tra validate trường Tên hoa | 17 |
| VALIDATION – Kiểm tra validate trường Loại hoa | 3 |
| VALIDATION – Kiểm tra validate trường Giá bán | 14 |
| VALIDATION – Kiểm tra validate trường Trạng thái hiển thị | 2 |
| VALIDATION – Kiểm tra validate trường Mô tả | 11 |
| VALIDATION – Kiểm tra validate trường Đường dẫn hình ảnh | 7 |
| UI – Giao diện mặc định | 17 |
| UI – Behavior | 25 |
| UI – Responsive | 2 |
| PHÂN QUYỀN – Quản trị viên được truy cập và thêm hoa mới | 1 |
| PHÂN QUYỀN – Khách vãng lai bị chặn khi thêm hoa mới | 2 |
| PHÂN QUYỀN – Thành viên bị chặn khi thêm hoa mới | 2 |
| ẢNH HƯỞNG – Danh sách sản phẩm hoa quản trị sau khi thêm mới | 1 |
| ẢNH HƯỞNG – Trang khách hàng sau khi thêm mới hoa | 8 |
| ẢNH HƯỞNG – Tìm kiếm sau khi thêm mới hoa | 2 |
| ẢNH HƯỞNG – Chi tiết sản phẩm và giỏ hàng với hoa vừa thêm | 2 |
| ẢNH HƯỞNG – Quản lý loại hoa sau khi thêm mới hoa | 1 |
| ẢNH HƯỞNG – Thống kê tổng quan sau khi thêm mới hoa | 2 |
| ẢNH HƯỞNG – Sửa sản phẩm hoa sau khi thêm mới | 1 |
| **Tổng** | **158** (HIGH 60 · MEDIUM 54 · LOW 44) |

### 12.3 Sửa hoa – Sửa sản phẩm hoa (`SUA_01…SUA_71`)

| Kịch bản chính | Số TC |
|---|---|
| FUNCTION – Mở màn hình Sửa sản phẩm hoa | 3 |
| FUNCTION – Cập nhật hoa thành công khi nhập dữ liệu hợp lệ | 11 |
| FUNCTION – Cập nhật hoa thất bại khi thiếu trường bắt buộc hoặc có trường không hợp lệ | 12 |
| FUNCTION – Tải lên, Làm lại và Quay lại trên màn hình Sửa sản phẩm hoa | 5 |
| FUNCTION – Ngoại lệ khi cập nhật sản phẩm hoa | 2 |
| VALIDATION – Kiểm tra validate các trường khi sửa sản phẩm hoa | 10 |
| UI – Giao diện mặc định | 5 |
| UI – Behavior | 6 |
| UI – Responsive | 2 |
| PHÂN QUYỀN – Khách vãng lai và Thành viên bị chặn khi sửa sản phẩm hoa | 4 |
| ẢNH HƯỞNG – Trang khách hàng và tìm kiếm sau khi sửa hoa | 6 |
| ẢNH HƯỞNG – Giỏ hàng và đơn hàng sau khi sửa hoa | 3 |
| ẢNH HƯỞNG – Thống kê và Quản lý loại hoa sau khi sửa hoa | 2 |
| **Tổng** | **71** (HIGH 48 · MEDIUM 10 · LOW 13) |

### 12.4 Xóa hoa – Xóa sản phẩm hoa (`XOA_01…XOA_24`)

| Kịch bản chính | Số TC |
|---|---|
| FUNCTION – Xóa sản phẩm hoa | 6 |
| UI – Giao diện mặc định | 3 |
| UI – Behavior | 3 |
| UI – Responsive | 1 |
| PHÂN QUYỀN – Khách vãng lai và Thành viên bị chặn khi xóa sản phẩm hoa | 2 |
| ẢNH HƯỞNG – Trang khách hàng và tìm kiếm sau khi xóa hoa | 4 |
| ẢNH HƯỞNG – Giỏ hàng và đơn hàng sau khi xóa hoa | 2 |
| ẢNH HƯỞNG – Thống kê và Quản lý loại hoa sau khi xóa hoa | 3 |
| **Tổng** | **24** (HIGH 17 · MEDIUM 0 · LOW 7) |

**Cả module: 282 TC** (HIGH 141 · MEDIUM 66 · LOW 75).

## Kết quả thực thi

| Lần chạy | Chức năng con | Ngày | Pass | Fail | Untested | Ghi chú |
|---|---|---|---|---|---|---|
| R1 | 12.1 Danh sách hoa | – | – | – | 29 | Chưa thực thi |
| R1 | 12.2 Thêm hoa | – | – | – | 158 | Chưa thực thi |
| R1 | 12.3 Sửa hoa | – | – | – | 71 | Chưa thực thi |
| R1 | 12.4 Xóa hoa | – | – | – | 24 | Chưa thực thi |

## Bug phát hiện

| Bug ID | Tiêu đề | Mức độ | TC liên quan |
|---|---|---|---|
| – | – | – | – |

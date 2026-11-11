# 12 – Quản lý sản phẩm hoa (`/quan-tri/hoa`)

[← Về trang chính](../../README.md)

## Mô tả chức năng

Quản trị viên thêm mới, sửa và xóa sản phẩm hoa.

| Chức năng con | SRS | Trạng thái |
|---|---|---|
| Thêm hoa mới (`/quan-tri/hoa/them`) | 4.3.4.1 | ✅ Test Design + Test Case (147 TC), chưa thực thi |
| Sửa sản phẩm hoa | 4.3.4.2 | ⬜ Chưa làm |
| Xóa sản phẩm hoa | 4.3.4.3 | ⬜ Chưa làm |

- **Tác nhân:** Quản trị viên (Khách vãng lai, Thành viên bị từ chối – lỗi 401)
- **Chức năng liên quan:** Quản lý loại hoa, Xem trang chủ & lọc hoa, Tìm kiếm, Chi tiết sản phẩm, Giỏ hàng, Thống kê tổng quan

## Quy tắc nghiệp vụ chính – Thêm hoa mới (đã confirm)

| Trường / Hành động | Quy tắc |
|---|---|
| Tên hoa | 5 – 20 ký tự (tính sau khi cắt khoảng trắng), chặn gõ quá 20; nhận chữ có dấu, chữ số và `.` `_` `;`; ký tự đặc biệt khác → coi như trống (FC_16) hoặc "Tên hoa không hợp lệ"; không nhận emoji; cắt khoảng trắng đầu/cuối; cho phép trùng tên |
| Giá bán | Chỉ nhập được số (không `,` `.`), 5.000 – 7.000.000 (gồm 2 mốc); bỏ số 0 đứng đầu và khoảng trắng; không định dạng trong ô nhập |
| Mô tả | Tối đa 250 ký tự (tính cả xuống dòng), chặn gõ quá 250, có bộ đếm; nhận ký tự đặc biệt và emoji |
| Đường dẫn hình ảnh | Chỉ cần là link, tối đa 500 ký tự (SRS), quá 500 → "Đường dẫn ảnh vượt quá 500 ký tự"; không phải link → "Đường dẫn ảnh không hợp lệ"; trống / ảnh lỗi → ảnh mặc định |
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

Chi tiết câu hỏi và trả lời: [qa-log.md](qa-log.md) (53 câu, đã confirm hết).

## Tài liệu

| Tài liệu | Xem online | File |
|---|---|---|
| Test Design (mindmap) | [test-design.md](test-design.md) | [test-design.xmind](test-design.xmind) |
| Test Case | – | [test-cases.xlsx](test-cases.xlsx) |

> Đã xong chức năng con **Thêm hoa mới**: Test Design 160 node lá, Test Case 147 TC (mọi node lá có ≥ 1 TC). Sửa / Xóa sản phẩm hoa: chưa làm.

## Thống kê Test Case – Thêm hoa mới

| Kịch bản chính | Số TC |
|---|---|
| 01. FUNCTION – Thêm hoa mới thành công khi nhập dữ liệu hợp lệ | 9 |
| 02. FUNCTION – Thêm hoa mới thất bại khi dữ liệu không hợp lệ | 3 |
| 03. FUNCTION – Kiểm tra đường dẫn ảnh bằng nút Tải lên | 6 |
| 04. FUNCTION – Làm lại form Thêm hoa mới | 3 |
| 05. FUNCTION – Điều hướng vào và ra màn hình Thêm hoa mới | 6 |
| 06. VALIDATION – Kiểm tra validate trường Tên hoa | 17 |
| 07. VALIDATION – Kiểm tra validate trường Loại hoa | 3 |
| 08. VALIDATION – Kiểm tra validate trường Giá bán | 14 |
| 09. VALIDATION – Kiểm tra validate trường Trạng thái hiển thị | 2 |
| 10. VALIDATION – Kiểm tra validate trường Mô tả | 11 |
| 11. VALIDATION – Kiểm tra validate trường Đường dẫn hình ảnh | 7 |
| 12. UI – Giao diện mặc định | 17 |
| 13. UI – Behavior | 25 |
| 14. UI – Responsive | 2 |
| 15. PHÂN QUYỀN – Quản trị viên được truy cập và thêm hoa mới | 1 |
| 16. PHÂN QUYỀN – Khách vãng lai bị chặn khi thêm hoa mới | 2 |
| 17. PHÂN QUYỀN – Thành viên bị chặn khi thêm hoa mới | 2 |
| 18. ẢNH HƯỞNG – Danh sách sản phẩm hoa quản trị sau khi thêm mới | 1 |
| 19. ẢNH HƯỞNG – Trang khách hàng sau khi thêm mới hoa | 8 |
| 20. ẢNH HƯỞNG – Tìm kiếm sau khi thêm mới hoa | 2 |
| 21. ẢNH HƯỞNG – Chi tiết sản phẩm và giỏ hàng với hoa vừa thêm | 2 |
| 22. ẢNH HƯỞNG – Quản lý loại hoa sau khi thêm mới hoa | 1 |
| 23. ẢNH HƯỞNG – Thống kê tổng quan sau khi thêm mới hoa | 2 |
| 24. ẢNH HƯỞNG – Sửa sản phẩm hoa sau khi thêm mới | 1 |
| **Tổng** | **147** (HIGH 49 · MEDIUM 54 · LOW 44) |

## Kết quả thực thi

| Lần chạy | Ngày | Pass | Fail | Untested | Ghi chú |
|---|---|---|---|---|---|
| R1 | – | – | – | – | Chưa thực thi |

## Bug phát hiện

| Bug ID | Tiêu đề | Mức độ | TC liên quan |
|---|---|---|---|
| – | – | – | – |

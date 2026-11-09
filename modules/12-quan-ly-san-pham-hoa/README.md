# 12 – Quản lý sản phẩm hoa (`/quan-tri/hoa`)

[← Về trang chính](../../README.md)

## Mô tả chức năng

Quản trị viên thêm mới, sửa và xóa sản phẩm hoa. Đang làm: **Thêm hoa mới** (`/quan-tri/hoa/them`, SRS 4.3.4.1).

- **Tác nhân:** Quản trị viên (Khách vãng lai, Thành viên bị từ chối – lỗi 401)
- **Chức năng liên quan:** Quản lý loại hoa, Xem trang chủ & lọc hoa, Tìm kiếm, Chi tiết sản phẩm, Giỏ hàng, Thống kê tổng quan

## Quy tắc nghiệp vụ chính – Thêm hoa mới (đã confirm)

| Trường / Hành động | Quy tắc |
|---|---|
| Tên hoa | 5 – 20 ký tự, chặn gõ quá 20; ký tự đặc biệt chỉ nhận `.` `_` `;`; không nhận emoji; cắt khoảng trắng đầu/cuối |
| Giá bán | Chỉ số, 5.000 – 7.000.000; không định dạng trong ô nhập; không hỗ trợ dấu phẩy |
| Mô tả | Tối đa 250 ký tự (tính cả xuống dòng), chặn gõ quá 250, có bộ đếm; nhận ký tự đặc biệt và emoji |
| Đường dẫn hình ảnh | Chỉ cần là link, không kiểm tra định dạng; trống / ảnh lỗi → ảnh mặc định |
| Nút Tải lên | Kiểm tra lấy được ảnh, tự điền đường dẫn, hỏi trước khi thay đường dẫn cũ; file JPG, PNG |
| Nút Làm lại | Loại hoa → "Hoa chia buồn"; Trạng thái → "Hiển thị" |
| Quay lại / tải lại trang / đóng tab khi đang nhập | Popup hỏi lưu thông tin |
| Thêm thành công | Chuyển về trang danh sách hoa |
| Nhiều trường lỗi | Báo lỗi tất cả các trường |
| Texthint | Theo SRS |

Chi tiết câu hỏi và trả lời: [qa-log.md](qa-log.md) (11 câu ❓ đang chờ BA/PO).

## Tài liệu

| Tài liệu | Xem online | File |
|---|---|---|
| Test Design (mindmap) | [test-design.md](test-design.md) | [test-design.xmind](test-design.xmind) |
| Test Case | – | [test-cases.xlsx](test-cases.xlsx) |

> Test Design và Test Case mới là file khung (chưa có node / TC).

## Thống kê Test Case

Chưa có.

## Kết quả thực thi

| Lần chạy | Ngày | Pass | Fail | Untested | Ghi chú |
|---|---|---|---|---|---|
| R1 | – | – | – | – | Chưa thực thi |

## Bug phát hiện

| Bug ID | Tiêu đề | Mức độ | TC liên quan |
|---|---|---|---|
| – | – | – | – |

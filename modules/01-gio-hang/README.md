# 01 – Giỏ hàng (`/gio-hang`)

[← Về trang chính](../../README.md)

## Mô tả chức năng

Người dùng xem và điều chỉnh danh sách sản phẩm trong giỏ hàng: tăng/giảm/nhập số lượng, xóa sản phẩm, cập nhật lại giá, xem tổng tiền và chuyển sang thanh toán.

- **Tác nhân:** Khách vãng lai, Thành viên, Quản trị viên
- **Chức năng liên quan:** Chi tiết sản phẩm & thêm vào giỏ, Thanh toán & đặt hàng, Đăng nhập, Quản trị sản phẩm hoa

## Quy tắc nghiệp vụ chính (đã confirm)

| Quy tắc | Giá trị |
|---|---|
| Số lượng tối đa / sản phẩm | 99 (đạt max thì nút (+) disable) |
| Số lượng = 1, bấm (−) | Về 0 và tự xóa sản phẩm khỏi giỏ |
| Số sản phẩm khác nhau tối đa | 20, phân trang 10 sản phẩm/trang |
| Xóa sản phẩm | Không có popup xác nhận |
| Sản phẩm bị ẩn | Ẩn khỏi giỏ, không tính vào tổng tiền |
| Nút "Cập nhật giỏ hàng" | Cập nhật lại giá khi giá sản phẩm thay đổi |
| Lưu giỏ hàng | Theo tài khoản |
| Tổng tiền | sum(đơn giá × số lượng), định dạng 150.000đ |

Chi tiết câu hỏi và trả lời: [qa-log.md](qa-log.md)

## Tài liệu

| Tài liệu | Xem online | File |
|---|---|---|
| Test Design (mindmap) | [test-design.md](test-design.md) | [test-design.xmind](test-design.xmind) |
| Test Case | [Google Sheets](https://docs.google.com/spreadsheets/d/1SoAGQ-Yi0rWPkkC3fgX_paQAvoOxCXqf/edit?gid=1901997707#gid=1901997707) | [test-cases.xlsx](test-cases.xlsx) |

<!-- Sau khi export ảnh mindmap từ XMind (File → Export → PNG), bỏ comment dòng dưới -->
<!-- ![Test Design – Giỏ hàng](test-design.png) -->

## Thống kê Test Case

| Nhóm | Kịch bản | Số TC |
|---|---|---|
| FUNCTION | Truy cập và hiển thị trang giỏ hàng | 6 |
| FUNCTION | Tăng số lượng bằng nút (+) | 7 |
| FUNCTION | Giảm số lượng bằng nút (−) | 6 |
| VALIDATION | Nhập trực tiếp số lượng từ bàn phím | 19 |
| FUNCTION | Xóa sản phẩm khỏi giỏ hàng | 4 |
| FUNCTION | Giới hạn số sản phẩm và phân trang | 10 |
| FUNCTION | Tính tiền và nút "Cập nhật giỏ hàng" | 6 |
| ẢNH HƯỞNG | Sản phẩm bị ẩn / bị xóa sau khi vào giỏ | 6 |
| FUNCTION | Lưu giỏ hàng theo tài khoản | 8 |
| FUNCTION | Thực hiện thanh toán từ giỏ hàng | 5 |
| PHÂN QUYỀN | Phân quyền truy cập giỏ hàng | 4 |
| ẢNH HƯỞNG | Ảnh hưởng và hồi quy các chức năng liên quan | 5 |
| UI | Giao diện mặc định | 7 |
| UI | Responsive | 1 |
| UI | Behavior | 15 |
| **Tổng** | | **109** (HIGH 66 · MEDIUM 20 · LOW 23) |

Theo nhóm: FUNCTION 52 · VALIDATION 19 · UI 23 · PHÂN QUYỀN 4 · ẢNH HƯỞNG 11. File theo template mới (giữ thứ tự kịch bản cũ, nên một nhóm có thể xuất hiện nhiều lần).

## Kết quả thực thi

| Lần chạy | Ngày | Pass | Fail | Untested | Ghi chú |
|---|---|---|---|---|---|
| R1 | – | – | – | 109 | Chưa thực thi |

## Bug phát hiện

| Bug ID | Tiêu đề | Mức độ | TC liên quan |
|---|---|---|---|
| – | – | – | – |

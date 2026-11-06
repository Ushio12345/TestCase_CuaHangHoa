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

| Kịch bản chính | Số TC |
|---|---|
| 01. Truy cập và hiển thị trang giỏ hàng | 6 |
| 02. Tăng số lượng bằng nút (+) | 7 |
| 03. Giảm số lượng bằng nút (−) | 6 |
| 04. Nhập trực tiếp số lượng (validation) | 19 |
| 05. Xóa sản phẩm | 4 |
| 06. Giới hạn số sản phẩm và phân trang | 10 |
| 07. Tính tiền và nút "Cập nhật giỏ hàng" | 6 |
| 08. Sản phẩm bị ẩn / bị xóa | 6 |
| 09. Lưu giỏ hàng theo tài khoản | 8 |
| 10. Thực hiện thanh toán | 5 |
| 11. Phân quyền | 4 |
| 12. Ảnh hưởng và hồi quy | 5 |
| 13. Giao diện | 8 |
| **Tổng** | **94** (HIGH 66 · MEDIUM 20 · LOW 8) |

## Kết quả thực thi

| Lần chạy | Ngày | Pass | Fail | Untested | Ghi chú |
|---|---|---|---|---|---|
| R1 | – | – | – | – | Chưa thực thi |

## Bug phát hiện

| Bug ID | Tiêu đề | Mức độ | TC liên quan |
|---|---|---|---|
| – | – | – | – |

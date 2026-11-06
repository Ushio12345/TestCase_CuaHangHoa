# SRS Review – Floral Charm v2.0

[← Về trang chính](../README.md)

Các điểm mâu thuẫn hoặc còn thiếu phát hiện khi phân tích SRS. Không bao gồm 11 lỗi cố ý được liệt kê trong phụ lục của SRS.

## 1. Mã thông báo lệch giữa các mục

| # | Vị trí | Vấn đề |
|---|---|---|
| 1 | Phụ lục – Bảng quy tắc kiểm tra | `ho_kh`, `ten_kh`, `sdt`, `dia_chi`: mã lỗi "để trống" và "nhập sai" bị đảo so với nội dung mã (VD: `ho_kh` để trống = FC_38 "Họ chứa chữ số") |
| 2 | Đăng ký – `ten_dn` | Mục Đăng ký: để trống = FC_01; Phụ lục: để trống = FC_02 |
| 3 | `mat_khau` | Lỗi để trống dùng FC_04, nhưng FC_04 là "sai độ dài" |
| 4 | Thêm sản phẩm hoa – `mo_ta` | Bảng trường dùng FC_23/FC_24, bảng lỗi dùng FC_25, Phụ lục dùng FC_24/FC_25 |
| 5 | `email` | Phụ lục: để trống = FC_40; mục Đăng ký: FC_09 |

## 2. Giới hạn giao diện khác cơ sở dữ liệu

| # | Trường | Giao diện | Cơ sở dữ liệu |
|---|---|---|---|
| 6 | `email` | Tối đa 50 ký tự | VARCHAR(100) |
| 7 | `dia_chi` / `noi_giao` | Tối đa 200 ký tự | VARCHAR(500) |
| 8 | `mo_ta` (hoa) | Bắt buộc | Cho phép NULL |

## 3. Thiếu hoặc chưa nhất quán

| # | Vị trí | Vấn đề |
|---|---|---|
| 9 | Thanh toán | "Ngày giao hàng mong muốn" không có cột lưu (`ngay_gh` là ngày đã giao) |
| 10 | Thanh toán | Phụ lục ghi `sdt` áp dụng cho Thanh toán, nhưng màn hình không có trường này |
| 11 | Cập nhật thông tin cá nhân | Bước 5 làm mới `/thanh-vien` thay vì `/tai-khoan` |
| 12 | Quy tắc nghiệp vụ | BR-04 dùng cho cả xóa loại hoa và xóa thành viên; BR-01, BR-02 không được định nghĩa |
| 13 | Đăng nhập quản trị | Tài khoản cài cứng chỉ nhắc ở mục chức năng, không có trong phụ lục lỗi |
| 14 | Phụ lục lỗi số 11 | `/api/orders` không gắn với chức năng nào (không có chức năng xem lịch sử đơn hàng) |
| 15 | Lỗi cố ý số 6 | Mục chức năng và phụ lục mô tả khác nhau |
| 16 | Xóa sản phẩm hoa | Xóa luôn `ct_don_dat_hang` liên quan → mất lịch sử đơn hàng |
| 17 | Kiểu dữ liệu | Giá tiền dùng FLOAT |
| 18 | Giỏ hàng | SRS ghi lưu ở bộ nhớ trình duyệt; BA/PO confirm lưu theo tài khoản; không có bảng lưu giỏ hàng |

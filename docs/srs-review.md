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
| 23 | Thêm sản phẩm hoa – `ten_hoa` | Bảng trường: để trống = FC_16; Phụ lục: để trống = FC_17 ("Tên hoa sai độ dài") |
| 24 | Thêm sản phẩm hoa – `gia` | Bảng trường: để trống = FC_20; Phụ lục: để trống = FC_21 ("Giá bán ngoài khoảng cho phép") |
| 25 | `mat_khau` – nhập sai | Đăng ký: FC_04 "phải từ 11 đến 30 ký tự"; Phụ lục: FC_41 "Mật khẩu mới phải tối thiểu 11 ký tự" (không nhắc tối đa 30) |
| 26 | `ho_kh` / `ten_kh` | Đăng ký dùng chung FC_05 / FC_06 ("Họ và tên…") cho cả 2 trường; Phụ lục tách riêng FC_38 (Họ) / FC_39 (Tên) |
| 27 | `sdt`, `email` – để trống | Không có thông báo "trống": Đăng ký dùng FC_07 / FC_09 ("… không hợp lệ"). FC_07 và FC_08, FC_09 và FC_40 trùng ý nghĩa |
| 28 | Thanh toán – địa chỉ | Phụ lục: `dia_chi` áp dụng cho Thanh toán với FC_11 / FC_12; mục Thanh toán: `diaChiGiaoHang` dùng FC_30 / FC_31. FC_31 "không hợp lệ" không nêu giới hạn 200 ký tự |

## 2. Giới hạn giao diện khác cơ sở dữ liệu

| # | Trường | Giao diện | Cơ sở dữ liệu |
|---|---|---|---|
| 6 | `email` | Tối đa 50 ký tự | VARCHAR(100) |
| 7 | `dia_chi` / `noi_giao` | Tối đa 200 ký tự | VARCHAR(500) |
| 8 | `mo_ta` (hoa) | Bắt buộc | Cho phép NULL |
| 29 | `ten_hoa` | 5 – 20 ký tự | VARCHAR(100) |
| 30 | `ten_dn` | 11 – 30 ký tự | VARCHAR(50) |
| 31 | `sdt` | 9 – 12 chữ số | VARCHAR(20) |
| 32 | `ma_loai` (hoa) | Bắt buộc | Không có NOT NULL |

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
| 19 | Thêm sản phẩm hoa – URL, tên nút | SRS: `/quan-tri/hoa`, nút "Lưu sản phẩm"; màn hình: `/quan-tri/hoa/them`, nút "Thêm mới" |
| 20 | Thêm sản phẩm hoa – `gia` | SRS: sự kiện "Thay đổi giá trị – định dạng tiền"; BA/PO confirm: không định dạng trong ô nhập, để nguyên số |
| 21 | Thêm sản phẩm hoa – nút | Màn hình có nút Tải lên, Làm lại, Quay lại; SRS không mô tả (hành vi lấy theo BA/PO, xem qa-log module 12) |
| 22 | Thêm sản phẩm hoa – `mo_ta` | SRS (sự kiện "đếm ký tự") và BA/PO: có bộ đếm ký tự; màn hình không có bộ đếm |
| 33 | `email` – độ dài tối thiểu | Phụ lục: 5 – 50 ký tự; mục Đăng ký chỉ ghi "tối đa 50 ký tự" |
| 34 | Tên bảng | Thiết kế CSDL: `DONDATHANG`, `CT_DONDATHANG`; luồng xử lý và cột khóa ngoại: `don_dat_hang`, `ct_don_dat_hang` |
| 35 | Giỏ hàng → Thanh toán | Giỏ hàng bước 5: nút "Thực hiện thanh toán"; Thanh toán bước 1: "chọn 'Thanh toán' từ trang giỏ hàng" (BA/PO chốt theo tên ở Giỏ hàng – qa-log 01 #21) |
| 36 | Giỏ hàng | Điều kiện tiên quyết "đã thêm ít nhất 1 sản phẩm", nhưng có màn hình "Giỏ hàng khi chưa có sản phẩm" |
| 37 | Đăng nhập khách hàng – `ten_dn` | Phụ lục áp quy tắc 11 – 30 ký tự, kiểm tra khi rời ô cho cả Đăng nhập; mục Đăng nhập chỉ kiểm tra khi bấm gửi biểu mẫu, quy tắc "tên đăng nhập đã đăng ký" |
| 38 | Thêm sản phẩm hoa | Bước 2 có nhập "đường dẫn ảnh" nhưng bảng trường không có `hinh_anh` |
| 39 | Sửa loại hoa | Không có kiểm tra trùng tên (FC_28) và giới hạn 100 ký tự như Thêm loại hoa |
| 40 | Cập nhật thông tin cá nhân | Không có bảng trường (trường nào được sửa, `email` có kiểm tra trùng không); FC_41 chỉ xuất hiện ở Phụ lục |
| 41 | Đăng tin tức | Không có bảng trường: `tieu_de` VARCHAR(200) không có giới hạn trên giao diện, `hinh_anh` không có quy tắc |
| 42 | Tin tức phía khách hàng | Ma trận phân quyền có "Xem tin tức", Đăng tin tức nhắc "Trang tin tức phía khách hàng", nhưng không có chức năng / URL tương ứng |
| 43 | Ma trận phân quyền | Không mô tả cách chặn (ẩn / chuyển hướng / thông báo) khi Thành viên vào Đăng ký / Đăng nhập, Quản trị viên vào Đăng ký / Đăng nhập / Thanh toán / Tài khoản; không có dòng cho Quản lý thành viên, Tin tức, Thống kê |
| 44 | Thông báo thành công | Đăng ký, đặt hàng, cập nhật, thêm / sửa / xóa chỉ ghi "hiển thị thông báo thành công", không có mã và nội dung trong Danh sách thông báo |
| 45 | Xóa đơn hàng, Xóa thành viên | Không có hộp thoại xác nhận (các chức năng xóa khác đều có) |
| 46 | Lỗi cố ý số 7 | Mục chức năng chỉ ghi ở Thêm loại hoa ("khách vãng lai gọi trực tiếp được"); Phụ lục: addProduct, addCategory, addNews, "bằng mã xác thực của khách hàng" |
| 47 | Thêm sản phẩm hoa – `ten_hoa` | SRS: trên 20 ký tự → FC_17; BA/PO: chặn gõ quá 20 → FC_17 chỉ còn cho trường hợp dưới 5 ký tự |
| 48 | Thêm sản phẩm hoa – `mo_ta` | SRS: trên 250 ký tự → FC_25 (bảng trường FC_24); BA/PO: chặn gõ ở 250 → thông báo "quá dài" không bao giờ hiện |
| 49 | Thêm sản phẩm hoa – sau khi lưu | SRS bước 5: "làm mới dữ liệu trang → hiển thị thông báo thành công"; BA/PO: chuyển về trang danh sách hoa |
| 50 | Thêm sản phẩm hoa – `hinh_anh` | CSDL: VARCHAR(500); BA/PO: đường dẫn ảnh không giới hạn độ dài (qa-log 12 #42). **BA/PO chốt (10/11):** theo SRS, tối đa 500 ký tự |
| 51 | Tìm kiếm sản phẩm hoa – bước 3 | SRS: tìm theo tên trong bảng `hoa`, không lọc `trang_thai`; BA/PO: hoa Ẩn không xuất hiện trong kết quả (qa-log 12 #45). **BA/PO chốt (10/11):** hoa Ẩn cũng không hiện trong danh sách hoa ở trang chủ của khách |
| 52 | Thêm sản phẩm hoa – `ten_hoa` | Danh sách thông báo không có mã cho lỗi "ký tự không hợp lệ" của Tên hoa; BA/PO: báo "không hợp lệ" (qa-log 12 #5, #47). **BA/PO chốt (10/11):** coi như để trống, hoặc bổ sung thông báo "Tên hoa không hợp lệ" |
| 53 | Thêm sản phẩm hoa – `hinh_anh` | Danh sách thông báo không có mã cho "đường dẫn ảnh quá dài" và "đường dẫn ảnh không hợp lệ"; BA/PO: "Đường dẫn ảnh vượt quá 500 ký tự", "Đường dẫn ảnh không hợp lệ" (qa-log 12 #22, #53) |

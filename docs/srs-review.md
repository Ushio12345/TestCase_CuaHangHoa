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
| 54 | Sửa sản phẩm hoa – màn hình | "Thiết kế màn hình: Không có", không có bảng trường; bước 2: "hộp thoại biểu mẫu", trong khi Thêm là trang riêng `/quan-tri/hoa/them` (qa-log 12 #54) |
| 55 | Sửa sản phẩm hoa – bước 4 | `UPDATE hoa SET ten_hoa=..., gia=...` không nêu đủ cột được cập nhật (`ma_loai`, `mo_ta`, `hinh_anh`, `trang_thai`, `ngay_d`?) (qa-log 12 #54, #57) |
| 56 | Sửa sản phẩm hoa – bước 5 | "Làm mới trang chi tiết và trang danh sách": phân hệ quản trị không có trang chi tiết sản phẩm |
| 57 | Xóa sản phẩm hoa – bước 4, 5 | 2 lệnh `DELETE FROM ct_don_dat_hang` và `DELETE FROM hoa` không yêu cầu giao dịch CSDL → lỗi ở lệnh 2 làm mất chi tiết đơn hàng mà hoa vẫn còn |
| 58 | Xóa sản phẩm hoa vs Xóa loại hoa / Xóa thành viên | Loại hoa đang có sản phẩm → chặn (FC_29); thành viên có đơn hàng → chặn (FC_34); hoa đã có trong đơn hàng → **xóa luôn** chi tiết đơn (xem #16) (qa-log 12 #64) |
| 59 | Xóa sản phẩm hoa – thông báo | FC_26 chỉ ghi "Lỗi cơ sở dữ liệu"; nội dung hộp thoại xác nhận và nút hủy không định nghĩa (chỉ có "Đồng ý xóa") (qa-log 12 #62, #65) |
| 60 | Danh sách sản phẩm hoa (`/quan-tri/hoa`) | Có ảnh màn hình "Trang quản lý sản phẩm hoa" nhưng không có mục chức năng: cột, sắp xếp, tìm kiếm, phân trang (qa-log 12 #67) |
| 61 | Sửa sản phẩm hoa – màn hình | SRS: "hộp thoại biểu mẫu"; BA/PO: trang riêng `/quan-tri/hoa/sua/[ma_hoa]`; SRS nút "Lưu thay đổi", BA/PO: "Cập nhật thông tin" (qa-log 12 #54, #56) |
| 62 | Xóa sản phẩm hoa – bước 4, 5 | SRS: `DELETE FROM ct_don_dat_hang` rồi `DELETE FROM hoa` (xóa cứng); BA/PO: hoa đã xóa vẫn hiển thị (làm mờ) trong đơn hàng → không thể xóa cứng chi tiết đơn. BA/PO chốt: **xóa mềm** – `trang_thai = 0`, không `DELETE` (qa-log 12 #64, #74) |
| 63 | Sửa / Xóa sản phẩm hoa – thông báo thành công | Không có mã trong Danh sách thông báo; BA/PO: popup "Tuyệt vời!" – "Thông tin hoa đã được cập nhật thành công!", "Đã xoá thành công" (bổ sung #44; qa-log 12 #57, #63) |
| 64 | Danh sách sản phẩm hoa – giá | SRS Định dạng tiền tệ: "150.000đ"; ảnh màn hình quản trị: "450.000 đ" (có khoảng trắng). BA/PO chốt theo SRS: "450.000đ" (qa-log 12 #73) |
| 65 | Xóa sản phẩm hoa – trạng thái `hoa.trang_thai` | Bảng `hoa`: `trang_thai` chỉ có 1 = Hiển thị, 0 = Ẩn; BA/PO: xóa mềm = `trang_thai = 0` → hoa đã xóa trùng hoa Ẩn. Mâu thuẫn: danh sách quản trị hiển thị hoa Ẩn (#73) vs xóa xong dòng biến mất (#63); Xóa loại hoa không tính hoa đã xóa (#75) nhưng không phân biệt được với hoa Ẩn; Tổng số hoa (Thống kê) có giảm sau khi xóa không (qa-log 12 #76) |
| 66 | Xem trang chủ & lọc hoa – luồng | Chỉ mô tả lọc theo loại; không mô tả nội dung trang chủ `/` (banner, "Thiết Kế Mới Nhất", "Hoa đặc biệt", khung Thành viên, Tìm kiếm nhanh) và `/hoa` khi không lọc (qa-log 02 #1 – #3). **BA/PO (19/11):** khung Thành viên, Tìm kiếm nhanh → module sau; "Thiết Kế Mới Nhất" 4 thẻ, mở rộng → 8 thẻ / trang; "Hoa đặc biệt" tạm fix cứng |
| 67 | Xem trang chủ & lọc hoa – màn hình | Ảnh `scr_02`, `scr_03` có ô "Sắp xếp: Mới nhất", dòng "N sản phẩm tinh hoa được tìm thấy", phân trang (1, 2, 3, Tiếp – chỉ nhắc ở lỗi cố ý số 2); SRS không có quy tắc (tùy chọn sắp xếp, số sản phẩm / trang) (qa-log 02 #4, #5, #8). **BA/PO chốt (19/11):** 8 sản phẩm / trang; sắp xếp Mới nhất, Giá tăng dần, Giá giảm dần; N = tổng số hoa trong bộ lọc |
| 68 | Xem trang chủ & lọc hoa – giá | SRS Định dạng tiền tệ: `150.000đ`; ảnh màn hình: `450.000 ₫` (có khoảng trắng, ký hiệu ₫) – cùng dạng #64 (qa-log 02 #10). **BA/PO chốt (19/11):** theo SRS `150.000đ` |
| 69 | Xem trang chủ & lọc hoa – bước 3 | SQL cố định `ma_loai = 1`; không có truy vấn cho `/hoa` (Tất cả các loại hoa), không nêu xử lý `?loai=` không hợp lệ / không tồn tại (qa-log 02 #12). **BA/PO chốt (19/11):** `?loai=` không hợp lệ → FC_36 |
| 70 | Xem trang chủ & lọc hoa – ảnh | Ảnh `scr_02`, `scr_03`: ảnh lỗi hiện chữ alt ("Dáng Ngọc Tinh Khôi", "Hoa Cưới Boho"); BA/PO (qa-log 12 #17): hiển thị ảnh mặc định (qa-log 02 #14). **BA/PO (19/11):** trang khách hiển thị tên hoa ở alt → mâu thuẫn 12 #17. **BA/PO chốt (19/11):** cả trang khách và trang quản lý, ảnh lỗi hoặc không có ảnh → alt = tên hoa, thay 12 #17 (qa-log 02 #25) |
| 71 | `hoa.ma_loai` – trang khách | Không NOT NULL (#32) → hoa không có loại có hiển thị ở "Tất cả các loại hoa" không, không thuộc mục nào trong Danh mục (qa-log 02 #13). **BA/PO chốt (19/11):** có hiển thị ở "Tất cả các loại hoa" |
| 72 | Danh mục loại hoa (trang khách) – thứ tự | BA/PO: Danh mục sắp theo thời gian tạo, trùng thì theo tên (qa-log 02 #22); bảng `loai_hoa` chỉ có `ma_loai`, `ten_loai`, không có cột ngày tạo (qa-log 02 #28). **BA/PO chốt (19/11):** loại mới thêm hiện cuối danh sách, không xét ngày tạo |
| 73 | Xem trang chủ & lọc hoa – phân trang | SRS (lỗi cố ý số 2): nút "1, 2, 3, Tiếp"; BA/PO: dạng `< 1 2 3 >`, trang 1 nút `<` disable (qa-log 02 #24); qa-log 02 #4: trang đầu / cuối **ẩn** nút (qa-log 02 #29). **BA/PO chốt (19/11):** `< 1 2 3 >`, trang 1 nút `<` disable, trang cuối nút `>` disable |
| 74 | Thêm / Sửa sản phẩm hoa – trả lời BA 25/11 | Trả lời mới lệch câu đã chốt: Tải lên có upload file JPG / PNG (đã chốt: chưa có); không kiểm tra link (đã chốt: "Đường dẫn ảnh không hợp lệ"); cấm hết ký tự đặc biệt ở `ten_hoa`, `mo_ta`, `hinh_anh` (đã chốt: danh sách ký tự được phép; link không thể thiếu `:` `/` `.`); trim mọi trường (đã chốt: chỉ Tên hoa); giá nhận `150.000` (đã chốt: chỉ gõ số); hoa bị xóa khi đang sửa vẫn lưu (đã chốt: báo lỗi); nội dung popup sửa thành công khác ảnh 17/11 (qa-log 12 #82 – #88) |

# Q&A – Xem trang chủ & lọc hoa (`/`, `/hoa`)

Câu hỏi làm rõ yêu cầu gửi BA/PO trong quá trình phân tích SRS và câu trả lời đã nhận. Các câu trả lời này là căn cứ cho Expected Result trong Test Design và Test Case.

**Trạng thái:** ✅ Đã confirm · ❓ Cần xác nhận thêm

<!-- Số # chỉ tăng, không chèn giữa, không đánh lại. Câu mới thêm ở cuối (mục "Bổ sung …" nếu cần). -->

## A. Trang chủ (`/`, sheet 02.1)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 1 | Phạm vi test của trang chủ gồm những khối nào (banner + nút "Khám phá ngay", "Thiết Kế Mới Nhất", Danh mục, khung Thành viên, Tìm kiếm nhanh, Hoa đặc biệt)? Khung Thành viên và Tìm kiếm nhanh thuộc module 06 / 03 hay test ở module 02? (srs-review #66) | Khung Thành viên và Tìm kiếm nhanh thực hiện ở module sau (ngoài phạm vi 02) | ✅ |
| 2 | "Thiết Kế Mới Nhất" hiển thị bao nhiêu hoa, sắp theo `ngay_d` giảm dần? "Hoa đặc biệt" chọn theo tiêu chí nào, bao nhiêu hoa? Nút "Khám phá ngay" chuyển đến đâu? | "Thiết Kế Mới Nhất": mặc định **4** thẻ; sau khi mở rộng (sổ ra toàn bộ) thì phân trang **8 thẻ / trang**. "Hoa đặc biệt": sẽ có danh sách riêng, hiện tạm **fix cứng**. Thứ tự sắp xếp, cách mở rộng, nút "Khám phá ngay": chưa trả lời → #17 – #19 | ✅ |
| 3 | Bấm một loại trong Danh mục ở trang chủ → chuyển sang `/hoa?loai=N` hay lọc tại chỗ? "Tất cả các loại hoa" → `/hoa`? | Danh mục ở trang chủ mặc định lọc "Tất cả các loại hoa"; bấm vào loại hoa → chuyển sang `/hoa` | ✅ |

## B. Danh sách & lọc hoa (`/hoa`, `/hoa?loai=N`, sheet 02.2)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 4 | Mỗi trang hiển thị bao nhiêu sản phẩm? Hành vi mong đợi của phân trang (ngoài lỗi cố ý số 2): URL có tham số trang không, nút "Tiếp" ở trang cuối, ẩn phân trang khi chỉ có 1 trang? (srs-review #67) | **8** sản phẩm / trang; URL có tham số trang; trang cuối ẩn nút "Tiếp", trang đầu ẩn nút về trang trước; chỉ có 1 trang → hiển thị trang "1" (#24 cập nhật: dạng `< 1 2 3 >`, trang 1 nút `<` disable) | ✅ |
| 5 | Ô "Sắp xếp" có những tùy chọn nào? Mặc định "Mới nhất" = `ngay_d` giảm dần? Đổi loại hoa thì giữ nguyên kiểu sắp xếp không? (srs-review #67) | 3 tùy chọn: **Mới nhất**, **Giá tăng dần**, **Giá giảm dần** (cột sắp xếp và giữ khi đổi loại: #20) | ✅ |
| 6 | Thẻ sản phẩm gồm: ảnh, tên loại, tên hoa, giá, icon giỏ hàng, nút "Thêm vào giỏ". Bấm ảnh / tên → `/hoa/[ma_hoa]`? Hai nút thêm vào giỏ test ở module 02 hay module 04? | Có, bấm ảnh / tên → `/hoa/[ma_hoa]`. Hai nút thêm vào giỏ: ở module 02 chỉ test badge giỏ hàng có cập nhật hay không | ✅ |
| 7 | Tên hoa dài bị cắt "…" (ảnh màn hình: "Dáng Ngọc Tinh…") – quy tắc cắt thế nào (1 dòng)? Có tooltip hiện tên đầy đủ không? | Có cắt, hiển thị **1 dòng** + "…" (tooltip: #21) | ✅ |
| 8 | Dòng "N sản phẩm tinh hoa được tìm thấy": N = tổng số hoa `trang_thai = 1` theo bộ lọc hiện tại (không phải số hoa trên trang)? | N = tổng số hoa trong bộ lọc | ✅ |
| 9 | Danh mục hiển thị toàn bộ `loai_hoa`, kể cả loại chưa có hoa? Thứ tự theo `ma_loai` tăng dần (như qa-log 12 #25)? Loại đang chọn được tô sáng? | Hiển thị **tất cả** loại hoa; loại chưa có hoa → trang trống (FC_36, xem #11) (thứ tự, tô sáng: #22) | ✅ |
| 10 | Định dạng giá theo SRS `150.000đ` hay theo màn hình `450.000 ₫`? (qa-log 12 #73 chốt theo SRS cho trang quản trị – áp dụng cả trang khách?) (srs-review #68) | Theo SRS: `150.000đ` | ✅ |
| 11 | FC_36 hiển thị ở đâu (thay cho lưới)? Dòng đếm = 0? Ẩn phân trang / ô sắp xếp không? "Tất cả các loại hoa" khi không có hoa nào hiển thị → FC_36 hay thông báo khác? | FC_36 **thay thế lưới** sản phẩm; **không hiện** dòng đếm (chỉ hiện khung thông báo); **ẩn** phân trang; **vẫn hiện** ô Sắp xếp ("Tất cả" khi không có hoa: #23) | ✅ |
| 12 | `?loai=` không hợp lệ (mã không tồn tại, 0, số âm, chữ, để trống, loại vừa bị xóa) → hiển thị FC_36, về "Tất cả", hay trang 404? (srs-review #69) | Hiển thị FC_36 | ✅ |
| 13 | Hoa có `ma_loai` NULL (CSDL cho phép) có hiện ở "Tất cả các loại hoa" không? (srs-review #32, #71) | Có hiển thị | ✅ |
| 14 | Ảnh trống / lỗi ở trang khách: hiển thị ảnh mặc định như qa-log 12 #17? (màn hình đang hiện chữ alt) (srs-review #70) | Hiển thị tên hoa ở alt (khác qa-log 12 #17: #25) | ✅ |

## C. Chung – Phân quyền & Ảnh hưởng

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 15 | Trang chủ sau khi đăng nhập (Thành viên – `scr_11`, Quản trị viên) khác khách vãng lai ở điểm nào (khung Thành viên đổi thành gì)? Quản trị viên có thấy hoa Ẩn ở trang khách không? | Đăng nhập thành công → khung Thành viên đổi thành khung thông tin tài khoản: avatar, "Chào, <tên>!", "THÀNH VIÊN THÂN THIẾT", "Quản lý tài khoản", "Đăng xuất" (ảnh BA gửi 19/11). Quản trị viên và hoa Ẩn: #26 | ✅ |
| 16 | Phạm vi chức năng bị ảnh hưởng – QA đề xuất: Quản lý sản phẩm hoa (thêm / sửa tên, giá, ảnh, loại / ẩn / xóa → lưới, dòng đếm, Thiết kế mới nhất), Quản lý loại hoa (thêm / đổi tên / xóa → Danh mục, lọc), Chi tiết sản phẩm (bấm thẻ), Giỏ hàng (thêm từ lưới). Đúng / thiếu? | Duyệt | ✅ |

## Bổ sung (19/11) – làm rõ câu trả lời #1 – #16

### A. Trang chủ

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 17 | (#2) "Thiết Kế Mới Nhất" 4 thẻ mặc định sắp theo `ngay_d` giảm dần? "Sổ ra toàn bộ" bằng nút nào (tên nút)? Mở rộng ngay tại trang chủ hay chuyển sang `/hoa`? Có thu gọn lại được không? | Có, 4 thẻ sắp theo ngày tạo mới nhất trước. Mở rộng bằng nút **"Xem toàn bộ sưu tập"** → chuyển sang `/hoa` (phân trang 8 thẻ / trang ở `/hoa`) | ✅ |
| 18 | (#2) Nút "Khám phá ngay" ở banner chuyển đến đâu (`/hoa`?) | Chuyển sang `/hoa` | ✅ |
| 19 | (#2) "Hoa đặc biệt" đang fix cứng: có test ở module 02 không? Nếu có: gồm những hoa nào, bấm vào → `/hoa/[ma_hoa]`? Hoa trong danh sách bị Ẩn / xóa thì còn hiện không? | Có test ở 02. Danh sách **đang fix cứng** (sau này sẽ có trường để lấy hoa đặc biệt) → không viết TC kiểm tra lấy đúng danh sách, ghi chú rõ "đang fix cứng". Bấm vào → trang chi tiết hoa đó (`/hoa/[ma_hoa]`). Hoa Ẩn / đã xóa không hiển thị | ✅ |

### B. Danh sách & lọc hoa

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 20 | (#5) "Mới nhất" = `ngay_d` giảm dần? Hai hoa cùng giá thì thứ tự phụ theo gì? Đổi loại hoa / chuyển trang thì giữ kiểu sắp xếp đang chọn hay về "Mới nhất"? | "Mới nhất" = theo ngày tạo (`ngay_d`), mới nhất trước; trùng ngày → theo tên hoa A–Z hoặc Z–A (chiều cụ thể, cùng giá, giữ khi đổi loại: #27) | ✅ |
| 21 | (#7) Rê chuột vào tên bị cắt có tooltip hiện tên đầy đủ không? | Có, hover vào tên hoa → tooltip hiện tên đầy đủ | ✅ |
| 22 | (#9) Danh mục sắp theo thứ tự nào (`ma_loai` tăng dần?) Loại đang chọn có được tô sáng không (ảnh `scr_03`: "Hoa Cưới" tô sáng)? | Có tô sáng loại đang chọn. Sắp theo thời gian tạo, trùng thì theo tên (chiều sắp, cột ngày tạo: #28) | ✅ |
| 23 | (#11) Chọn "Tất cả các loại hoa" khi không có hoa nào đang hiển thị → FC_36 hay thông báo khác? | FC_36 | ✅ |
| 24 | (#4) "Ẩn sau ở trang đầu" = ở trang 1 ẩn nút về trang trước? Nút này tên gì ("Trước"?) | Phân trang dạng `< 1 2 3 >`; ở trang 1 nút `<` bị **disable** (cập nhật #4: "ẩn" → disable; trang cuối: #29) | ✅ |
| 25 | (#14) Ảnh lỗi ở trang khách hiển thị tên hoa ở alt, trong khi qa-log 12 #17 chốt "ảnh mặc định" cho cả trang quản lý và trang khách. Trang khách theo câu trả lời mới (alt)? Trang quản lý vẫn giữ ảnh mặc định? (srs-review #70) | Cả trang khách và trang quản lý: ảnh lỗi hoặc không có ảnh → hiển thị **alt = tên hoa** (thay câu trả lời qa-log 12 #17 "ảnh mặc định") | ✅ |

### C. Chung

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 26 | (#1, #15) Khung thông tin tài khoản sau đăng nhập có thuộc "module sau" như khung Thành viên (#1) không, hay test ở 02? Quản trị viên mở trang khách thì khung hiển thị gì, có thấy hoa Ẩn không? | Chỉ test hiển thị: đã đăng nhập → khung thông tin tài khoản (#15); chưa đăng nhập → ô đăng nhập. Chức năng của khung ở module sau (Quản trị viên: #30) | ✅ |

## Bổ sung (19/11) – làm rõ câu trả lời #17 – #26

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 27 | (#20) Hai hoa trùng ngày tạo: sắp theo tên **A–Z** hay **Z–A** (cố định chiều nào)? Sắp "Giá tăng / giảm dần" mà hai hoa cùng giá thì xếp theo gì? Đổi loại hoa / chuyển trang thì giữ kiểu sắp xếp đang chọn hay về "Mới nhất"? | Trùng ngày tạo hoặc cùng giá → sắp theo tên hoa **A → Z** (mọi kiểu sắp xếp). Đổi loại hoa / chuyển trang → **giữ** kiểu sắp xếp đang chọn | ✅ |
| 28 | (#22) Danh mục sắp theo thời gian tạo **tăng** hay **giảm** dần? Bảng `loai_hoa` không có cột ngày tạo (chỉ `ma_loai`, `ten_loai`) → QA kiểm tra bằng `ma_loai`? (srs-review #72) | Loại mới thêm hiện **cuối** danh sách (thêm vào cuối, không xét ngày tạo) → thứ tự theo thứ tự thêm (`ma_loai` tăng dần) | ✅ |
| 29 | (#4, #24) Ở trang cuối, nút `>` bị **disable** (như `<` ở trang 1) hay **ẩn** (#4)? | Có, trang cuối nút `>` **disable** | ✅ |
| 30 | (#26) Quản trị viên đã đăng nhập trang quản trị rồi mở trang khách (`/`, `/hoa`): khung bên phải hiển thị ô đăng nhập hay thông tin tài khoản? | Hiển thị **ô đăng nhập** (trang khách coi như chưa đăng nhập) | ✅ |

# Q&A – Quản lý sản phẩm hoa (`/quan-tri/hoa`)

Câu hỏi làm rõ yêu cầu gửi BA/PO trong quá trình phân tích SRS và câu trả lời đã nhận. Các câu trả lời này là căn cứ cho Expected Result trong Test Design và Test Case.

**Trạng thái:** ✅ Đã confirm · ❓ Cần xác nhận thêm

## A. Thêm hoa mới (`/quan-tri/hoa/them`, SRS 4.3.4.1)

### 1. Tên hoa (`ten_hoa`)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 1 | Ký tự đặc biệt nào được chấp nhận? | `.` `_` `;` `-` `,` `:` `(` `)` `/` `'` (nháy đơn). BA chốt lại 17/11 – lần trước: chỉ `.` `_` `;` | ✅ |
| 2 | Dấu cách ở đầu và cuối có được cắt bỏ không? | Có (chỉ áp dụng cho Tên hoa) | ✅ |
| 3 | Nhập quá 20 ký tự thì chặn gõ hay báo lỗi? | Chặn, không cho nhập quá 20 ký tự | ✅ |
| 4 | Có chấp nhận icon (emoji) không? | Không (emoji chỉ chấp nhận ở Mô tả) | ✅ |
| 5 | Nhập ký tự đặc biệt bị chặn thì chặn gõ hay báo lỗi (mã nào)? Chữ có dấu và chữ số có được chấp nhận không? | Chấp nhận chữ có dấu và chữ số; ký tự đặc biệt khác → báo "không hợp lệ" (mã / nội dung chính xác: xem #47) | ✅ |
| 6 | Tên hoa có được trùng với hoa đã có không (CSDL không có UNIQUE)? Nếu không, thông báo lỗi là gì? | Cho phép trùng | ✅ |
| 7 | Tên hoa chỉ nhập khoảng trắng: sau khi cắt thì tính là để trống (FC_16) hay báo lỗi khác? | Tính là để trống → FC_16 | ✅ |

### 2. Giá bán (`gia`)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 8 | Ký tự được chấp nhận và khoảng giá? | Chỉ số, từ 5.000 đến 7.000.000 | ✅ |
| 9 | Định dạng tiền áp dụng ngay trong ô nhập không? Có hậu tố "đ" không? | Không định dạng, để nguyên số; đơn vị tính là VNĐ | ✅ |
| 10 | Nhập `5,000` / `5,5` (dấu phẩy, kiểu châu Âu) thì xử lý thế nào? | Không hỗ trợ | ✅ |
| 11 | Nhập dấu phẩy, chữ, số âm, số thập phân thì chặn gõ hay báo FC_21? 5.000 và 7.000.000 có hợp lệ không? | 5.000 và 7.000.000 hợp lệ; chỉ cho nhập số, không nhập được `,` hay `.` | ✅ |

### 3. Mô tả (`mo_ta`)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 12 | Ký tự đặc biệt và emoji? | Không giới hạn ký tự đặc biệt; chấp nhận emoji | ✅ |
| 13 | Có hiển thị bộ đếm ký tự không? Quá 250 ký tự thì chặn gõ hay báo lỗi? | Có bộ đếm; chặn ở 250 ký tự | ✅ |
| 14 | Ký tự xuống dòng có tính vào giới hạn 250 ký tự không? | Có, tính tất cả ký tự | ✅ |

### 4. Đường dẫn hình ảnh và nút Tải lên

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 15 | Ký tự trong đường dẫn (`: / ? & = % # _ - .`) có bị chặn không? | Không chặn | ✅ |
| 16 | Có kiểm tra định dạng đường dẫn, đuôi file ảnh không? | Không, chỉ cần là link | ✅ |
| 17 | Để trống hoặc ảnh không tải được thì hiển thị gì (trang quản lý và trang khách)? | Hiển thị ảnh mặc định | ✅ |
| 18 | Nút Tải lên (không có trong SRS) hoạt động thế nào? | Nhập URL, bấm Tải lên → kiểm tra có lấy được ảnh không | ✅ |
| 19 | Tải lên thành công có tự điền vào ô Đường dẫn hình ảnh không? | Có | ✅ |
| 20 | Ô đã có đường dẫn mà tải lên ảnh khác thì lấy giá trị nào? | Hỏi có muốn thay thế đường dẫn không | ✅ |
| 21 | Định dạng file ảnh được chấp nhận? | ~~JPG, PNG~~ → BA chốt lại (#51): mọi link ảnh hợp lệ | ✅ |
| 22 | Nhập chữ không phải link, link không lấy được ảnh, hoặc tải file không phải JPG/PNG thì thông báo lỗi là gì? | Thông báo "Đường dẫn ảnh không hợp lệ" (hiện chưa có upload file – #23) | ✅ |
| 23 | Tải lên là chọn file từ máy hay kiểm tra URL đã nhập (#18 và #21 khác nhau)? Nút có bị vô hiệu hóa mặc định (chữ mờ) không? | Tải lên chỉ kiểm tra đường dẫn có hợp lệ không; hiện chưa cho upload file (trạng thái mặc định của nút: xem #48) | ✅ |

### 5. Loại hoa và Trạng thái hiển thị

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 24 | SRS ghi bắt buộc, màn hình không đánh dấu `*` và cả hai có giá trị mặc định → bắt buộc hay không? | Có, bắt buộc | ✅ |
| 25 | Danh sách loại hoa lấy từ đâu (bảng `loai_hoa`?), sắp xếp theo thứ tự nào? | Cần có TC; SRS là bản mẫu nên QA tự đề xuất kết quả hợp lý. QA đề xuất: toàn bộ loại hoa trong bảng `loai_hoa`, sắp xếp theo `ma_loai` tăng dần | ✅ |
| 26 | Danh sách trạng thái lấy từ đâu? | Như #25. QA đề xuất: 2 lựa chọn cố định "Hiển thị" (1) / "Ẩn" (0) theo SRS (bảng `HOA`, cột `trang_thai`) | ✅ |

### 6. Nút và luồng màn hình

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 27 | Texthint trên màn hình khác SRS → theo bên nào? | Theo SRS | ✅ |
| 28 | Nút Làm lại (không có trong SRS) đưa các trường về giá trị nào? | Loại hoa: "Hoa chia buồn"; Trạng thái: chọn nút "Hiển thị" | ✅ |
| 29 | Làm lại có xóa trắng các ô nhập và các thông báo lỗi đang hiển thị không? | Có | ✅ |
| 30 | Nút Quay lại về trang nào? Đã nhập dữ liệu chưa lưu thì có cảnh báo không? | Về trang danh sách hoa; có popup hỏi lưu thông tin | ✅ |
| 31 | Đang nhập dở rồi tải lại trang hoặc đóng tab thì dữ liệu giữ hay mất? | Có popup hỏi lưu; chọn không thì không lưu | ✅ |
| 32 | Thêm mới thành công thì ở lại hay chuyển trang? Nút Thêm mới có bị vô hiệu hóa khi đang gửi không? | Chuyển về trang danh sách hoa. ~~Nút Thêm mới không bị vô hiệu hóa~~ → BA chốt lại (#50): khóa nút khi đang xử lý | ✅ |
| 33 | Nội dung, vị trí, thời gian tự ẩn của thông báo thành công? Nội dung popup hỏi lưu thông tin? | Thông báo tự ẩn sau 5 giây hoặc khi người dùng bấm tắt (nội dung, vị trí, popup: xem #49) | ✅ |
| 34 | Nhiều trường cùng không hợp lệ thì báo lỗi tất cả hay chỉ trường đầu tiên? | Báo lỗi tất cả các trường | ✅ |

### 7. Bổ sung khi thiết kế test

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 35 | Để trống Tên hoa / Giá / Mô tả hiện mã nào: bảng trường (FC_16 / FC_20 / FC_23) hay Phụ lục (FC_17 / FC_21 / FC_24)? (srs-review #4, #23, #24) | Hiện mã lỗi theo bảng trường của từng trường: Tên hoa FC_16, Giá FC_20, Mô tả FC_23 | ✅ |
| 36 | Paste chuỗi dài hơn giới hạn (Tên hoa > 20, Mô tả > 250 ký tự) thì cắt bớt hay không nhận cả chuỗi? | Một trong hai cách đều được: tự cắt về đúng giới hạn, hoặc báo lỗi và chặn gửi form | ✅ |
| 37 | Mô tả chỉ có khoảng trắng / xuống dòng (Mô tả không được cắt khoảng trắng – #2) có tính là để trống không? | Có, tính là để trống | ✅ |
| 38 | Độ dài Tên hoa (5 – 20) tính trước hay sau khi cắt khoảng trắng đầu/cuối? | Tính sau khi cắt khoảng trắng | ✅ |
| 39 | Bấm Thêm mới nhiều lần liên tiếp (nút không bị vô hiệu hóa – #32) thì tạo 1 hay nhiều bản ghi? | Chỉ tạo 1 bản ghi; chặn bấm liên tục (khác #32: xem #50) | ✅ |
| 40 | Giá có số 0 đứng đầu (`05000`) hoặc khoảng trắng đầu/cuối thì xử lý thế nào? | Bỏ số 0 đứng đầu; tự loại bỏ khoảng trắng đầu/cuối | ✅ |
| 41 | Phiên quản trị hết hạn khi đang nhập rồi bấm Thêm mới → chuyển về trang đăng nhập? Dữ liệu đã nhập giữ hay mất? | Chuyển về trang đăng nhập; dữ liệu đã nhập bị mất | ✅ |
| 42 | Đường dẫn hình ảnh có giới hạn độ dài không (CSDL VARCHAR(500))? | Tối đa 500 ký tự theo SRS (CSDL VARCHAR(500)). BA chốt lại 10/11 – lần trước trả lời "Không giới hạn" (srs-review #50) | ✅ |
| 43 | Tên nút lưu: theo SRS "Lưu sản phẩm" hay màn hình "Thêm mới"? (srs-review #19) | Theo màn hình: "Thêm mới" | ✅ |
| 44 | Hoa mới hiển thị ở vị trí nào trong danh sách quản trị (sắp xếp theo tiêu chí nào)? | Hiển thị đầu tiên | ✅ |
| 45 | Hoa có trạng thái Ẩn có xuất hiện trong kết quả Tìm kiếm không? (SRS Tìm kiếm không lọc `trang_thai`) | Không xuất hiện; hoa Ẩn cũng không hiện trong danh sách hoa ở trang chủ của khách (srs-review #51) | ✅ |
| 46 | Thẻ "Tổng số hoa" ở Thống kê tổng quan có đếm cả hoa Ẩn không? | Có, đếm cả hoa Ẩn | ✅ |

### 8. Bổ sung sau câu trả lời BA (10/11)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 47 | (#5) Tên hoa nhập ký tự đặc biệt không được phép: mã và nội dung thông báo "không hợp lệ" chính xác là gì? (SRS không có mã cho lỗi ký tự của Tên hoa) | Coi như để trống, hoặc bổ sung thông báo "Tên hoa không hợp lệ" (srs-review #52) | ✅ |
| 48 | (#23) Khi mở form, nút Tải lên có bị vô hiệu hóa (chữ mờ) không? Khi nào thì bấm được? | Chỉ bấm được khi ô Đường dẫn hình ảnh đã có nội dung | ✅ |
| 49 | (#33) Nội dung và vị trí của thông báo thêm thành công? Nội dung popup hỏi lưu thông tin? | Nội dung đã có trên màn hình, chỉ cần kiểm tra đúng; tắt thông báo thành công thì chuyển sang trang danh sách sản phẩm | ✅ |
| 50 | (#32 – #39) "Chặn bấm liên tục" là khóa nút Thêm mới khi đang xử lý (khác #32 "nút không bị vô hiệu hóa"), hay nút vẫn bấm được nhưng chỉ xử lý 1 lần? | Khóa nút Thêm mới khi đang xử lý (thay cho #32 "không bị vô hiệu hóa") | ✅ |
| 51 | (#21 – #23) Không có upload file thì "JPG, PNG" (#21) nghĩa là đường dẫn phải trỏ tới ảnh JPG / PNG? Khác #16 "không kiểm tra đuôi file" | Chấp nhận mọi link ảnh hợp lệ, không giới hạn JPG / PNG (thay cho #21) | ✅ |
| 52 | Khi mở form, Loại hoa mặc định chọn giá trị nào? (Làm lại đưa về "Hoa chia buồn" – #28) | Giá trị đầu tiên trong danh sách | ✅ |
| 53 | (#42) Đường dẫn ảnh dài hơn 500 ký tự: chặn gõ / tự cắt hay báo lỗi (mã, nội dung)? | Báo lỗi "Đường dẫn ảnh vượt quá 500 ký tự" | ✅ |

## B. Sửa sản phẩm hoa (SRS 4.3.4.2)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 54 | Form sửa là hộp thoại (popup) hay trang riêng (URL nào)? Sửa được những trường nào (cả 6 trường như Thêm)? (srs-review #54, #55) | Trang riêng `/quan-tri/hoa/sua/[ma_hoa]` (VD `/quan-tri/hoa/sua/83`), đủ các trường như Thêm | ✅ |
| 55 | Mọi quy tắc và câu trả lời của Thêm (#1–#53: chặn gõ, cắt khoảng trắng, mã lỗi, Tải lên, nhiều lỗi báo tất cả…) có áp dụng y hệt cho Sửa không? | Có | ✅ |
| 56 | Form sửa có những nút nào (Lưu thay đổi, Hủy / Đóng, Làm lại, Tải lên)? "Làm lại" đưa về dữ liệu cũ hay xóa trắng? Đóng form khi đã đổi dữ liệu thì có hỏi lưu không? | Nút lưu tên "Cập nhật thông tin"; các nút khác giống Thêm (Làm lại, Quay lại, Tải lên); Làm lại giống Thêm (xóa trắng ô nhập, Loại hoa "Hoa chia buồn", Trạng thái "Hiển thị") | ✅ |
| 57 | Lưu thành công: nội dung thông báo? Ở lại danh sách hay chuyển trang? Hoa vừa sửa nằm ở vị trí nào trong danh sách? `ngay_d` có đổi không? | Hiện popup: biểu tượng ✓, tiêu đề "Tuyệt vời!", nội dung "Thông tin hoa đã được cập nhật thành công!", nút "ĐÓNG CỬA SỔ". Đóng popup → về danh sách hoa; hoa vừa sửa giữ vị trí, `ngay_d` không đổi (QA hiểu từ trả lời "không") | ✅ |
| 58 | Bấm "Lưu thay đổi" khi không sửa gì thì báo gì, có ghi CSDL không? | Có: vẫn ghi CSDL và hiện popup cập nhật thành công | ✅ |
| 59 | Sửa hoa đã bị xóa (ở tab khác / bởi quản trị viên khác) thì thông báo gì? | QA đề xuất (BA đồng ý): mở `/quan-tri/hoa/sua/[id]` của hoa không tồn tại → không hiện form, báo "Không tìm thấy sản phẩm" (hoặc 404); đang sửa mà hoa bị xóa ở tab khác, bấm Cập nhật → báo lỗi, không tạo bản ghi mới, về danh sách | ✅ |
| 60 | Sửa giá: đơn hàng cũ giữ `gia_ban` cũ? Giỏ hàng của thành viên đổi giá ngay hay chờ "Cập nhật giỏ hàng" (liên quan qa-log 01 #15)? | Giỏ hàng đổi giá ngay; đơn hàng cũ giữ `gia_ban` cũ (SRS CSDL `CT_DONDATHANG.gia_ban`) | ✅ |

## C. Xóa sản phẩm hoa (SRS 4.3.4.3)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 61 | "Chọn sản phẩm hoa rồi bấm Xóa": nút Xóa trên từng dòng, hay chọn nhiều (checkbox) để xóa hàng loạt? | Nút Xóa trên từng dòng | ✅ |
| 62 | Hộp thoại xác nhận xóa: nội dung, tên nút hủy? Esc / bấm ra ngoài có đóng hộp thoại không? (srs-review #59) | Nội dung: "Bạn có thực sự muốn xóa sản phẩm này không?"; nút hủy: "Huỷ"; Esc / bấm ra ngoài không đóng hộp thoại | ✅ |
| 63 | Xóa thành công: nội dung thông báo? Xóa hoa duy nhất ở trang cuối thì danh sách về trang nào? | Thông báo "Đã xoá thành công"; xóa hoa duy nhất ở trang cuối → vẫn ở trang đó, hiển thị trống hoặc gợi ý thêm hoa | ✅ |
| 64 | Hoa đã có trong đơn hàng: vẫn cho xóa (SRS xóa `ct_don_dat_hang`) hay chặn như Xóa loại hoa / Xóa thành viên? Đơn hàng mất hết chi tiết thì còn hiển thị ở Quản lý đơn hàng không, tổng tiền thế nào? (srs-review #16, #58) | Vẫn cho xóa. Trong đơn hàng, hoa đã xóa vẫn hiển thị nhưng ẩn / làm mờ; hoa đã xóa nằm trong giỏ → khi thanh toán hiển thị thông báo yêu cầu xóa sản phẩm khỏi giỏ (srs-review #62; cách lưu CSDL: #74) | ✅ |
| 65 | FC_26 "Không thể xóa sản phẩm này" xảy ra khi nào (hoa đã bị xóa trước, lỗi CSDL…)? QA tái hiện bằng cách nào? | Tạm bỏ qua (chưa viết TC cho FC_26) | ✅ |
| 66 | Mở `/hoa/[id]` của hoa đã xóa → lỗi 404 như hoa Ẩn? Hoa đã xóa đang nằm trong giỏ thành viên thì xử lý thế nào (liên quan qa-log 01 #16)? | Giỏ hàng: như #64; mở `/hoa/[id]` của hoa đã xóa → 404 | ✅ |

## D. Chung

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 67 | Màn hình danh sách `/quan-tri/hoa` (cột, sắp xếp, tìm kiếm, phân trang) có thuộc phạm vi test module 12 không? Nếu có, quy tắc là gì? (srs-review #60) | Có, thuộc phần hiển thị danh sách hoa của module 12. SRS không có quy tắc (chỉ có ảnh màn hình `scr_17_admin_hoa.png`) → QA đề xuất theo ảnh; điểm chưa rõ: #69 – #73 | ✅ |
| 68 | Phạm vi chức năng bị ảnh hưởng khi Sửa / Xóa hoa – QA đề xuất: trang khách (`/`, `/hoa`, lọc theo loại), Tìm kiếm, Chi tiết sản phẩm, Giỏ hàng, Thanh toán, Quản lý đơn hàng, Quản lý loại hoa (xóa loại sau khi hết hoa), Thống kê tổng quan. Đúng / thiếu? | Đúng | ✅ |

## E. Bổ sung sau câu trả lời BA (17/11)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 69 | (#67) Ô "Tìm kiếm tên hoa": khớp một phần hay toàn bộ tên? Có phân biệt chữ hoa / thường, có dấu / không dấu? Tìm khi bấm "Áp dụng" hay cả khi nhấn Enter? Ô trống + "Áp dụng" → toàn bộ danh sách? Không có kết quả thì hiển thị gì? | Khớp một phần tên; không phân biệt chữ hoa / thường và có dấu / không dấu; tìm khi bấm "Áp dụng" hoặc nhấn Enter; ô trống → toàn bộ danh sách; không có kết quả → danh sách rỗng | ✅ |
| 70 | (#67) "Lọc theo loại" gồm "Tất cả loại hoa" + toàn bộ loại trong `loai_hoa`? Tìm kiếm và lọc có áp dụng đồng thời khi bấm "Áp dụng" không? | Có: "Tất cả loại hoa" + toàn bộ loại trong `loai_hoa`; tìm kiếm và lọc áp dụng đồng thời | ✅ |
| 71 | (#67) Danh sách sắp xếp theo tiêu chí nào: `ma_hoa` giảm dần (hoa mới lên đầu – #44, hoa vừa sửa giữ vị trí – #57)? | Theo thời gian tạo (`ngay_d`), mới nhất lên đầu (QA hiểu chiều giảm dần theo #44); hoa vừa sửa giữ vị trí vì `ngay_d` không đổi (#57) | ✅ |
| 72 | (#67) Danh sách có phân trang không? Bao nhiêu dòng mỗi trang? | Có phân trang, 20 sản phẩm / trang | ✅ |
| 73 | (#67) Danh sách quản trị có hiển thị hoa Ẩn không, cột Trạng thái của hoa Ẩn hiển thị thế nào? Giá hiển thị "450.000 đ" (ảnh màn hình) hay "450.000đ" (SRS Định dạng tiền tệ)? (srs-review #64) | Có hiển thị hoa Ẩn, cột Trạng thái hiển thị "Ẩn"; giá theo SRS: "450.000đ" (ảnh "450.000 đ" là sai lệch) | ✅ |
| 74 | (#64) Xóa hoa là xóa cứng (SRS: `DELETE` bảng `hoa` và `ct_don_dat_hang`) hay xóa mềm (để hoa vẫn hiển thị làm mờ trong đơn hàng)? Sau khi xóa, QA kiểm tra CSDL thế nào? (srs-review #62) | Xóa mềm: cập nhật trạng thái hoa thành Ẩn (`trang_thai = 0`), không `DELETE` bảng `hoa` / `ct_don_dat_hang`. QA kiểm tra: `SELECT trang_thai FROM hoa WHERE ma_hoa = …` = 0, `ct_don_dat_hang` vẫn còn dòng của hoa (phân biệt với hoa Ẩn: #76) | ✅ |

## F. Bổ sung sau trả lời #69 – #74 (17/11)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 75 | (#74) Sau khi xóa (mềm) hoa duy nhất của một loại, bản ghi hoa vẫn còn trong bảng `hoa` → Xóa loại hoa có bị chặn "loại còn sản phẩm" (FC_29) không? | Hoa đã xóa không tính khi kiểm tra loại còn sản phẩm | ✅ |
| 76 | (#63, #73, #74, #75) Hoa đã xóa và hoa Ẩn cùng `trang_thai = 0` → hệ thống không phân biệt được: (1) danh sách quản trị hiển thị hoa Ẩn (#73) → hoa vừa xóa còn trong danh sách với trạng thái "Ẩn", hay biến mất (#63)? (2) Xóa loại hoa: hoa Ẩn chưa xóa có được tính là "loại còn sản phẩm" không (#75)? (3) Thống kê: Tổng số hoa có giảm 1 sau khi xóa không (Thêm hoa Ẩn làm Tổng số hoa tăng 1)? Cần giá trị / cột riêng cho "Đã xóa"? (srs-review #65) | – | ❓ |

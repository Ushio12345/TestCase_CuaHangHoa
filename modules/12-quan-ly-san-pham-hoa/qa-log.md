# Q&A – Quản lý sản phẩm hoa (`/quan-tri/hoa`)

Câu hỏi làm rõ yêu cầu gửi BA/PO trong quá trình phân tích SRS và câu trả lời đã nhận. Các câu trả lời này là căn cứ cho Expected Result trong Test Design và Test Case.

**Trạng thái:** ✅ Đã confirm · ❓ Cần xác nhận thêm

## A. Thêm hoa mới (`/quan-tri/hoa/them`, SRS 4.3.4.1)

### 1. Tên hoa (`ten_hoa`)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 1 | Ký tự đặc biệt nào được chấp nhận? | Chỉ `.` `_` `;` | ✅ |
| 2 | Dấu cách ở đầu và cuối có được cắt bỏ không? | Có (chỉ áp dụng cho Tên hoa) | ✅ |
| 3 | Nhập quá 20 ký tự thì chặn gõ hay báo lỗi? | Chặn, không cho nhập quá 20 ký tự | ✅ |
| 4 | Có chấp nhận icon (emoji) không? | Không (emoji chỉ chấp nhận ở Mô tả) | ✅ |
| 5 | Nhập ký tự đặc biệt bị chặn thì chặn gõ hay báo lỗi (mã nào)? Chữ có dấu và chữ số có được chấp nhận không? | – | ❓ |
| 6 | Tên hoa có được trùng với hoa đã có không (CSDL không có UNIQUE)? Nếu không, thông báo lỗi là gì? | – | ❓ |
| 7 | Tên hoa chỉ nhập khoảng trắng: sau khi cắt thì tính là để trống (FC_16) hay báo lỗi khác? | – | ❓ |

### 2. Giá bán (`gia`)

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 8 | Ký tự được chấp nhận và khoảng giá? | Chỉ số, từ 5.000 đến 7.000.000 | ✅ |
| 9 | Định dạng tiền áp dụng ngay trong ô nhập không? Có hậu tố "đ" không? | Không định dạng, để nguyên số; đơn vị tính là VNĐ | ✅ |
| 10 | Nhập `5,000` / `5,5` (dấu phẩy, kiểu châu Âu) thì xử lý thế nào? | Không hỗ trợ | ✅ |
| 11 | Nhập dấu phẩy, chữ, số âm, số thập phân thì chặn gõ hay báo FC_21? 5.000 và 7.000.000 có hợp lệ không? | – | ❓ |

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
| 21 | Định dạng file ảnh được chấp nhận? | JPG, PNG | ✅ |
| 22 | Nhập chữ không phải link, link không lấy được ảnh, hoặc tải file không phải JPG/PNG thì thông báo lỗi là gì? | – | ❓ |
| 23 | Tải lên là chọn file từ máy hay kiểm tra URL đã nhập (#18 và #21 khác nhau)? Nút có bị vô hiệu hóa mặc định (chữ mờ) không? | – | ❓ |

### 5. Loại hoa và Trạng thái hiển thị

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 24 | SRS ghi bắt buộc, màn hình không đánh dấu `*` và cả hai có giá trị mặc định → bắt buộc hay không? | – | ❓ |
| 25 | Danh sách loại hoa lấy từ đâu (bảng `loai_hoa`?), sắp xếp theo thứ tự nào? | – | ❓ |
| 26 | Danh sách trạng thái lấy từ đâu? | – | ❓ |

### 6. Nút và luồng màn hình

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 27 | Texthint trên màn hình khác SRS → theo bên nào? | Theo SRS | ✅ |
| 28 | Nút Làm lại (không có trong SRS) đưa các trường về giá trị nào? | Loại hoa: "Hoa chia buồn"; Trạng thái: chọn nút "Hiển thị" | ✅ |
| 29 | Làm lại có xóa trắng các ô nhập và các thông báo lỗi đang hiển thị không? | – | ❓ |
| 30 | Nút Quay lại về trang nào? Đã nhập dữ liệu chưa lưu thì có cảnh báo không? | Về trang danh sách hoa; có popup hỏi lưu thông tin | ✅ |
| 31 | Đang nhập dở rồi tải lại trang hoặc đóng tab thì dữ liệu giữ hay mất? | Có popup hỏi lưu; chọn không thì không lưu | ✅ |
| 32 | Thêm mới thành công thì ở lại hay chuyển trang? Nút Thêm mới có bị vô hiệu hóa khi đang gửi không? | Chuyển về trang danh sách hoa; nút Thêm mới không bị vô hiệu hóa | ✅ |
| 33 | Nội dung, vị trí, thời gian tự ẩn của thông báo thành công? Nội dung popup hỏi lưu thông tin? | – | ❓ |
| 34 | Nhiều trường cùng không hợp lệ thì báo lỗi tất cả hay chỉ trường đầu tiên? | Báo lỗi tất cả các trường | ✅ |

### 7. Bổ sung khi thiết kế test

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 35 | Để trống Tên hoa / Giá / Mô tả hiện mã nào: bảng trường (FC_16 / FC_20 / FC_23) hay Phụ lục (FC_17 / FC_21 / FC_24)? (srs-review #4, #23, #24) | – | ❓ |
| 36 | Paste chuỗi dài hơn giới hạn (Tên hoa > 20, Mô tả > 250 ký tự) thì cắt bớt hay không nhận cả chuỗi? | – | ❓ |
| 37 | Mô tả chỉ có khoảng trắng / xuống dòng (Mô tả không được cắt khoảng trắng – #2) có tính là để trống không? | – | ❓ |
| 38 | Độ dài Tên hoa (5 – 20) tính trước hay sau khi cắt khoảng trắng đầu/cuối? | – | ❓ |
| 39 | Bấm Thêm mới nhiều lần liên tiếp (nút không bị vô hiệu hóa – #32) thì tạo 1 hay nhiều bản ghi? | – | ❓ |
| 40 | Giá có số 0 đứng đầu (`05000`) hoặc khoảng trắng đầu/cuối thì xử lý thế nào? | – | ❓ |
| 41 | Phiên quản trị hết hạn khi đang nhập rồi bấm Thêm mới → chuyển về trang đăng nhập? Dữ liệu đã nhập giữ hay mất? | – | ❓ |
| 42 | Đường dẫn hình ảnh có giới hạn độ dài không (CSDL VARCHAR(500))? | – | ❓ |
| 43 | Tên nút lưu: theo SRS "Lưu sản phẩm" hay màn hình "Thêm mới"? (srs-review #19) | – | ❓ |
| 44 | Hoa mới hiển thị ở vị trí nào trong danh sách quản trị (sắp xếp theo tiêu chí nào)? | – | ❓ |
| 45 | Hoa có trạng thái Ẩn có xuất hiện trong kết quả Tìm kiếm không? (SRS Tìm kiếm không lọc `trang_thai`) | – | ❓ |
| 46 | Thẻ "Tổng số hoa" ở Thống kê tổng quan có đếm cả hoa Ẩn không? | – | ❓ |

# Q&A – Giỏ hàng (`/gio-hang`)

Câu hỏi làm rõ yêu cầu gửi BA/PO trong quá trình phân tích SRS và câu trả lời đã nhận. Các câu trả lời này là căn cứ cho Expected Result trong Test Design và Test Case.

**Trạng thái:** ✅ Đã confirm · ❓ Cần xác nhận thêm

## 1. Số lượng sản phẩm

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 1 | Có giới hạn số lượng tối đa cho 1 sản phẩm trong giỏ không? | Có, tối đa **99**. Khi đạt 99 thì nút (+) bị disable | ✅ |
| 2 | Có cho nhập trực tiếp số lượng từ bàn phím không? | Có | ✅ |
| 3 | Spam thêm vào giỏ nhiều lần thì hệ thống cho tăng hay chặn? | Tăng bình thường tới max (99) thì dừng | ✅ |
| 4 | Thêm cùng sản phẩm (cộng dồn) vượt max thì xử lý thế nào? | Vẫn thông báo thêm vào giỏ thành công, nhưng số lượng trong giỏ không tăng | ✅ |
| 5 | Số lượng đang là 1, bấm (−) thì disable nút hay xóa sản phẩm? | Cập nhật số lượng = 0 rồi tự động xóa sản phẩm khỏi giỏ | ✅ |
| 6 | SRS cho giảm về 0 và số âm, nhưng web chặn cứng ở 1? | Theo SRS và câu trả lời số 5 | ✅ |
| 7 | Nhập số lượng 0, số âm, trên 99, để trống, chữ, số thập phân thì xử lý thế nào? | – | ❓ |

## 2. Danh sách sản phẩm trong giỏ

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 8 | Có giới hạn tổng số sản phẩm khác nhau trong 1 giỏ không? | Có, tối đa **20** sản phẩm, phân trang **10 sản phẩm/trang** | ✅ |
| 9 | Khi xóa sản phẩm có popup xác nhận không? | Không có | ✅ |
| 10 | Có xem được chi tiết sản phẩm từ giỏ hàng không? | Không cho xem | ✅ |
| 11 | Thêm sản phẩm thứ 21 thì xử lý thế nào? | – | ❓ |
| 12 | Xóa sản phẩm duy nhất ở trang 2 thì có tự quay về trang 1 không? | – | ❓ |

## 3. Giá và trạng thái sản phẩm

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 13 | Nút (+)/(−) đã tự tính lại tiền, vậy nút "Cập nhật giỏ hàng" dùng để làm gì? | Cập nhật lại giá khi giá thay đổi mà người dùng không biết (ví dụ khuyến mãi bất chợt) | ✅ |
| 14 | Sản phẩm đã trong giỏ bị ẩn thì xử lý thế nào? | Ẩn khỏi giỏ hàng, không tính vào tổng tiền | ✅ |
| 15 | Giá đã đổi nhưng chưa bấm "Cập nhật giỏ hàng" thì giỏ và trang thanh toán dùng giá nào? | – | ❓ |
| 16 | Sản phẩm bị ẩn rồi hiện lại, hoặc bị Admin xóa, thì giỏ xử lý thế nào? | – | ❓ |

## 4. Lưu giỏ hàng và đăng nhập

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 17 | Giỏ hàng lưu theo tài khoản hay theo trình duyệt? | Theo tài khoản (tài khoản B không thấy giỏ của tài khoản A) | ✅ |
| 18 | Guest đang ở trang giỏ hàng rồi đăng nhập thì ở lại giỏ hay về trang chủ? | Giữ nguyên ở trang giỏ hàng | ✅ |
| 19 | Guest thêm sản phẩm rồi đăng nhập thì giỏ được gộp, bỏ hay thay? | – | ❓ |
| 20 | Mở giỏ ở 2 tab, thay đổi ở 1 tab thì tab kia có đồng bộ không? | – | ❓ |

## 5. Khác

| # | Câu hỏi | Trả lời | Trạng thái |
|---|---|---|---|
| 21 | Tên nút trên màn hình khác SRS ("Tiến hành thanh toán" / "Thêm vào giỏ") – kiểm tra theo đâu? | Theo SRS: "Thực hiện thanh toán", "Thêm vào giỏ hàng" | ✅ |
| 22 | SRS ghi chọn số lượng ở trang chi tiết, nhưng màn hình không có ô số lượng? | Bug của màn hình chi tiết sản phẩm; ảnh hưởng một số case thêm vào giỏ | ✅ |
| 23 | Popup "đã thêm vào giỏ hàng" có thuộc phạm vi giỏ hàng không? | Không, thuộc chức năng thêm vào giỏ | ✅ |
| 24 | Badge trên icon giỏ hàng đếm tổng số lượng hay số sản phẩm khác nhau? | Số sản phẩm khác nhau (VD: SP1 SL 5 + SP2 SL 2 → badge 2) | ✅ |
| 25 | Nội dung khung giỏ hàng trống? | Icon giỏ hàng, text "Giỏ hàng của bạn đang trống...", nút "THÊM SẢN PHẨM VÀO GIỎ" | ✅ |

# Test Plan – Floral Charm

[← Về trang chính](../README.md)

## 1. Mục tiêu

Kiểm thử chức năng hệ thống bán hoa trực tuyến Floral Charm theo SRS v2.0, phát hiện lỗi về nghiệp vụ, dữ liệu, phân quyền và giao diện.

## 2. Phạm vi

| Trong phạm vi | Ngoài phạm vi |
|---|---|
| 15 chức năng của phân hệ Khách hàng và Quản trị (xem bảng tiến độ ở README) | Kiểm thử hiệu năng, tải |
| Kiểm thử chức năng, validation, giao diện, phân quyền, ảnh hưởng | Kiểm thử bảo mật chuyên sâu (pentest) |
| Kiểm tra dữ liệu bằng SQL (nếu có quyền truy cập DB) | Kiểm thử tự động |

## 3. Phương pháp

- Manual testing, black-box
- Kỹ thuật: Equivalence Partitioning, Boundary Value Analysis, State Transition, Decision Table, Error Guessing
- Mỗi chức năng đi theo quy trình: Phân tích SRS → Q&A → Test Design → Test Case → Thực thi → Bug Report

## 4. Môi trường

| Hạng mục | Giá trị |
|---|---|
| URL | https://training-web-flower-sale.vercel.app |
| Trình duyệt | Chrome bản mới nhất (desktop) |
| Thiết bị phụ | Kích thước tablet 768px, mobile 375px (Chrome DevTools) |
| Cơ sở dữ liệu | PostgreSQL |

## 5. Vai trò test

Khách vãng lai · Thành viên (tài khoản test) · Quản trị viên (tài khoản test). Thông tin đăng nhập không lưu trong repo.

## 6. Quy ước Priority

| Loại kiểm thử | Priority |
|---|---|
| Chức năng chính, Phân quyền, Ảnh hưởng | HIGH |
| Validation | MEDIUM |
| Giao diện | LOW |

## 7. Tiêu chí

- **Bắt đầu:** SRS đã được phân tích, các câu hỏi quan trọng đã có câu trả lời, dữ liệu test đã chuẩn bị
- **Kết thúc:** 100% test case HIGH đã thực thi; mọi bug Critical/Major đã được ghi nhận

## 8. Sản phẩm bàn giao

Test Design (XMind) · Test Case (Excel) · Q&A log · Bug list · Báo cáo kết quả trong README từng chức năng

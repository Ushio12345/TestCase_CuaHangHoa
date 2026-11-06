# 🌸 Floral Charm – Manual Testing Portfolio

> Dự án thực hành kiểm thử phần mềm thủ công trên hệ thống bán hoa trực tuyến **Floral Charm**: phân tích SRS, đặt câu hỏi làm rõ yêu cầu, thiết kế Test Design (mindmap), viết Test Case, thực thi và báo cáo lỗi.

![Status](https://img.shields.io/badge/status-in%20progress-yellow) ![Type](https://img.shields.io/badge/testing-manual-blue) ![Modules](https://img.shields.io/badge/modules-1%2F15%20done-green)

---

## Giới thiệu dự án

| Hạng mục           | Nội dung                                                                 |
| ------------------ | ------------------------------------------------------------------------ |
| Hệ thống           | Floral Charm – website thương mại điện tử bán hoa tươi                   |
| Phân hệ            | Khách hàng (cửa hàng) · Quản trị                                         |
| Vai trò người dùng | Khách vãng lai · Thành viên · Quản trị viên                              |
| Môi trường test    | Web Chrome (desktop) – https://training-web-flower-sale.vercel.app       |
| Tài liệu đầu vào   | SRS Floral Charm v2.0 (tài liệu đào tạo, không đính kèm trong repo)      |
| Vai trò của tôi    | Manual QA – thực hiện toàn bộ quy trình từ phân tích yêu cầu đến báo cáo |

> Đây là ứng dụng phục vụ đào tạo kiểm thử, được cài sẵn một số lỗi có chủ đích.

---

## Kỹ năng thể hiện

- **Phân tích yêu cầu:** đọc SRS, phát hiện điểm mâu thuẫn / thiếu, lập danh sách câu hỏi Q&A gửi BA/PO
- **Test Design:** mindmap theo nhóm Function · Validation · UI · Phân quyền · Ảnh hưởng (XMind)
- **Kỹ thuật thiết kế test:** Equivalence Partitioning, Boundary Value Analysis, State Transition, Decision Table, Error Guessing
- **Viết Test Case:** Pre-conditions, Test Steps, Test Data, Expected Result theo từng step, Priority
- **Kiểm tra dữ liệu:** câu lệnh SQL (PostgreSQL) verify dữ liệu sau thao tác
- **Bug Report:** mô tả lỗi, bước tái hiện, mức độ nghiêm trọng, bằng chứng

---

## 📊 Tiến độ theo chức năng

**Chú thích:** ✅ Hoàn thành · 🟡 Đang làm · ⬜ Chưa bắt đầu

### Phân hệ Khách hàng

| #   | Chức năng                                               | Test Design                                   | Test Case                                                                                                                               | Số TC | Trạng thái |
| --- | ------------------------------------------------------- | --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ----- | ---------- |
| 01  | [Giỏ hàng](modules/01-gio-hang/README.md) (`/gio-hang`) | [Mindmap](modules/01-gio-hang/test-design.md) | [Google Sheets](https://docs.google.com/spreadsheets/d/1KgZI0jVNESa4P1WYLJnznRT4CGR7Mzlww-tiGYN7k_E/edit?gid=1373814062#gid=1373814062) | 94    | ✅         |
| 02  | Xem trang chủ & lọc hoa (`/`, `/hoa`)                   | –                                             | –                                                                                                                                       | –     | ⬜         |
| 03  | Tìm kiếm sản phẩm (`/tim-kiem`)                         | –                                             | –                                                                                                                                       | –     | ⬜         |
| 04  | Chi tiết sản phẩm & thêm vào giỏ (`/hoa/[id]`)          | –                                             | –                                                                                                                                       | –     | ⬜         |
| 05  | Đăng ký tài khoản (`/dang-ky`)                          | –                                             | –                                                                                                                                       | –     | ⬜         |
| 06  | Đăng nhập khách hàng (`/dang-nhap`)                     | –                                             | –                                                                                                                                       | –     | ⬜         |
| 07  | Thanh toán & đặt hàng (`/thanh-toan`)                   | –                                             | –                                                                                                                                       | –     | ⬜         |
| 08  | Cập nhật thông tin cá nhân (`/tai-khoan`)               | –                                             | –                                                                                                                                       | –     | ⬜         |

### Phân hệ Quản trị

| #   | Chức năng            | Test Design | Test Case | Số TC | Trạng thái |
| --- | -------------------- | ----------- | --------- | ----- | ---------- |
| 09  | Đăng nhập quản trị   | –           | –         | –     | ⬜         |
| 10  | Thống kê tổng quan   | –           | –         | –     | ⬜         |
| 11  | Quản lý loại hoa     | –           | –         | –     | ⬜         |
| 12  | Quản lý sản phẩm hoa | –           | –         | –     | ⬜         |
| 13  | Quản lý đơn đặt hàng | –           | –         | –     | ⬜         |
| 14  | Quản lý thành viên   | –           | –         | –     | ⬜         |
| 15  | Quản lý tin tức      | –           | –         | –     | ⬜         |

---

## Quy trình làm việc

```
SRS  →  Phân tích & Q&A với BA/PO  →  Test Design (XMind)  →  Test Case (Excel)  →  Thực thi  →  Bug Report
```

1. **Phân tích SRS:** xác định luồng nghiệp vụ, quy tắc dữ liệu, phân quyền, điểm chưa rõ
2. **Q&A:** ghi nhận câu hỏi và câu trả lời đã confirm → làm căn cứ cho Expected Result
3. **Test Design:** mindmap phân cấp, bao phủ Positive / Negative / Boundary / Exception
4. **Test Case:** triển khai từ mindmap, gom theo kịch bản chính, gán Priority
5. **Thực thi & báo cáo:** ghi Actual Result, Pass/Fail, liên kết Bug ID

---

## Tài liệu chung

- [Test Plan](docs/test-plan.md) – phạm vi, phương pháp, môi trường, tiêu chí
- [SRS Review](docs/srs-review.md) – các điểm mâu thuẫn / thiếu phát hiện trong SRS
- [Bug List](bug-reports/bug-list.xlsx) – danh sách lỗi phát hiện

---

## Cấu trúc repository

```
floral-charm-qa/
├── README.md
├── docs/
│   ├── test-plan.md            # Phạm vi, môi trường, tiêu chí bắt đầu/kết thúc
│   └── srs-review.md           # Các điểm mâu thuẫn / thiếu phát hiện trong SRS
├── modules/
│   ├── 01-gio-hang/
│   │   ├── README.md           # Tóm tắt chức năng, quy tắc đã confirm, kết quả
│   │   ├── qa-log.md           # Câu hỏi & câu trả lời BA/PO
│   │   ├── test-design.xmind   # File gốc
│   │   ├── test-design.png     # Ảnh xem nhanh trên GitHub
│   │   ├── test-design.md      # Outline dạng text
│   │   └── test-cases.xlsx     # Bản tải về (bản xem online: Google Sheets)
│   ├── 02-trang-chu-loc-hoa/
│   └── ...
└── bug-reports/
    └── bug-list.xlsx
```

---

## Tổng hợp kết quả

| Chỉ số            | Giá trị |
| ----------------- | ------- |
| Tổng số Test Case | 94      |
| Đã thực thi       | –       |
| Pass / Fail       | – / –   |
| Số bug phát hiện  | –       |

_(Cập nhật sau mỗi đợt chạy test)_

---

## Công cụ

XMind · Microsoft Excel / Google Sheets · Chrome DevTools · Postman

---

## 👤 Tác giả

**[Huynh Thi Que Anh]** – Manual Tester
📧 [anhqueht1100@gmail.com]

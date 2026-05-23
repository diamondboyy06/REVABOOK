# SƠ ĐỒ TÍNH NĂNG HỆ THỐNG REVABOOK (FEATURE MAP)

Tài liệu này định nghĩa chi tiết các tính năng của hệ thống, được phân quyền theo 4 nhóm tác nhân (Actors) chính: Độc giả (User), Tác giả/Nhà xuất bản (Creator), Nhân viên (Staff/Moderator) và Quản trị viên cấp cao (Admin).

---

## 1. Độc giả / Thính giả (User)
*Người dùng cuối sử dụng Mobile App để tiêu thụ nội dung.*

*   **Tài khoản & Hồ sơ (Account & Profile):**
    *   Đăng ký / Đăng nhập (Email, Google, Apple, Facebook).
    *   Quản lý thông tin cá nhân, cài đặt ngôn ngữ và sở thích.
*   **Khám phá Nội dung (Discovery / Marketplace):**
    *   Tìm kiếm sách/truyện theo từ khóa, tác giả, thể loại.
    *   Lọc theo định dạng (Sách chữ, Truyện tranh), ngôn ngữ lồng tiếng.
    *   Gợi ý sách dựa trên lịch sử đọc/nghe (Recommendation Engine).
*   **Cửa hàng & Thanh toán (Store & Wallet):**
    *   Nạp tiền vào Ví (Coin/Credit) qua In-App Purchase (IAP) hoặc Payment Gateway.
    *   Mua đứt (Buy) hoặc Thuê (Rent) sách/truyện.
    *   Xem lịch sử giao dịch.
*   **Trình phát Thông minh (Smart Player):**
    *   **Sách chữ:** Nghe audio, tự động cuộn trang, **Highlight text đồng bộ theo giọng đọc**. Tùy chỉnh tốc độ phát (0.5x - 2.0x).
    *   **Truyện tranh:** Chế độ lật trang thủ công (Manual Turn), audio tự động khớp với trang/bong bóng thoại đang xem.
    *   Tải xuống để nghe/đọc Offline (có bảo vệ DRM).
*   **Tương tác (Interaction):**
    *   Đánh giá (Rating), bình luận (Review) sách.
    *   **Báo lỗi (Feedback):** Bôi đen đoạn text/audio bị lỗi (dịch sai, đọc vấp) và gửi Report cho Tác giả.

---

## 2. Tác giả / Nhà xuất bản (Creator)
*Người tạo và sở hữu bản quyền nội dung, sử dụng Creator Studio (Web/PC App).*

*   **Quản lý Nội dung (Content Management):**
    *   Tạo dự án Sách mới, phân loại (Text/Comic).
    *   Upload bản thảo (File text/Word) hoặc hình ảnh (ZIP/PDF).
    *   Quản lý danh sách Chương (Chapters).
*   **AI Studio & Quy trình Sản xuất (Production Workflow):**
    *   Kích hoạt tiến trình phân tích tự động (OCR/NLP).
    *   Lựa chọn ngôn ngữ muốn dịch (Đa ngôn ngữ).
    *   Gán giọng đọc AI cho từng nhân vật.
    *   Kích hoạt quá trình Dịch thuật & Lồng tiếng hàng loạt (Batch Processing).
*   **Sửa lỗi Tương tác (Interactive AI Correction):**
    *   Xem danh sách Báo cáo lỗi (Reports) từ Độc giả.
    *   **AI Chat Agent:** Mở khung chat với AI, ra lệnh sửa lỗi cục bộ (VD: "Dịch lại câu này", "Đổi giọng đọc"). Nhấn "Apply" để lưu đè bản sửa lỗi.
*   **Kinh doanh & Phân tích (Sales & Analytics):**
    *   Thiết lập giá bán, giá thuê.
    *   Xem Dashboard thống kê: Lượt xem, lượt nghe, doanh thu theo thời gian thực.
    *   Yêu cầu Rút tiền (Withdraw) doanh thu về tài khoản ngân hàng.

---

## 3. Nhân viên / Kiểm duyệt viên (Staff / Moderator)
*Đội ngũ vận hành của hệ thống, sử dụng Internal Admin Tool.*

*   **Kiểm duyệt Nội dung (Content Moderation):**
    *   Duyệt (Approve) hoặc Từ chối (Reject) sách/truyện mới trước khi Public lên Marketplace (Kiểm tra vi phạm bản quyền, nội dung nhạy cảm 18+, bạo lực).
    *   Xử lý các Report vi phạm nội dung từ cộng đồng.
*   **Hỗ trợ Khách hàng (Customer Support - CS):**
    *   Giải quyết khiếu nại của User (Lỗi nạp tiền, không tải được sách).
    *   Giải quyết ticket của Creator.
*   **Quản lý Chất lượng (QA - Quality Assurance):**
    *   Nghe/đọc kiểm tra ngẫu nhiên các bản dịch/lồng tiếng AI để đánh giá chất lượng hệ thống.

---

## 4. Quản trị viên Hệ thống (System Admin)
*Người có quyền hạn cao nhất, quản lý toàn bộ nền tảng.*

*   **Dashboard Tổng quan (Global Dashboard):**
    *   Theo dõi "Sức khỏe" hệ thống (System Health), số lượng User online, tổng doanh thu nền tảng.
*   **Quản lý Tài chính (Financial Management):**
    *   Cấu hình tỷ lệ hoa hồng (Commission Rate) của nền tảng (VD: Nền tảng lấy 30%, Tác giả nhận 70%).
    *   Duyệt các lệnh rút tiền lớn của Creator.
*   **Quản lý Tác nhân (User & Staff Management):**
    *   Khóa/Mở khóa (Ban/Unban) tài khoản User hoặc Creator vi phạm.
    *   Tạo tài khoản Staff, phân quyền (Role-based access control) cho từng nhân viên (VD: Chỉ được duyệt sách, không được xem tài chính).
*   **Cấu hình Hệ thống (System Config):**
    *   Quản lý API Keys của các dịch vụ bên thứ 3 (ElevenLabs, OpenAI, Stripe, v.v.).
    *   Điều chỉnh cấu hình AI (Ví dụ: Chuyển đổi Model AI để tiết kiệm chi phí).










fheuhuehuehufe
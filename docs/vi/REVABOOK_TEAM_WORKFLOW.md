# CẤU TRÚC ĐỘI NGŨ & QUY TRÌNH PHÁT TRIỂN (TEAM & WORKFLOW)

Tài liệu này định nghĩa cấu trúc nhân sự và quy trình phát triển cho dự án REVABOOK, được thiết kế bằng cách **kết hợp mô hình Xoắn ốc (Spiral Model) và phương pháp luận Agile/Scrum**.

## 1. Triết lý Vận hành: Spiral-Agile Hybrid

Hệ thống REVABOOK chứa nhiều rủi ro kỹ thuật cao (Xử lý AI bất đồng bộ, Đồng bộ Audio-Text, DRM). Do đó, chúng ta kết hợp:
- **Vĩ mô (Macro-level) - Mô hình Xoắn ốc:** Định hướng từng Phase lớn (Phase 1, Phase 2) dựa trên việc đánh giá rủi ro và làm Prototype. Nếu PoC (Proof of Concept) thất bại, vòng xoắn ốc sẽ dừng lại để đánh giá trước khi code thật.
- **Vi mô (Micro-level) - Agile/Scrum:** Trong mỗi Phase lớn, công việc được chia nhỏ thành các Sprint (1-2 tuần). Đội ngũ sẽ code, test liên tục và giao hàng (delivery) những phần mềm chạy được cuối mỗi Sprint.

## 2. Cấu trúc Đội ngũ (Team Structure & Roles)

Để vận hành trơn tru quy trình trên, đội ngũ được phân định vai trò rõ ràng như sau:

### A. Nhóm Quản trị & Chiến lược (The Steering Team)
Tập trung vào Vòng lặp Xoắn ốc (Lập kế hoạch & Phân tích rủi ro).

*   **1. Product Owner (PO - Chủ sản phẩm):**
    *   *Vai trò:* "Tiếng nói của Khách hàng". Người quyết định tính năng nào làm trước, tính năng nào làm sau.
    *   *Nhiệm vụ:* Quản lý Product Backlog (Danh sách tính năng), nghiệm thu sản phẩm cuối cùng.
*   **2. Solution Architect / Data Architect (Kiến trúc sư Hệ thống):**
    *   *Vai trò:* Người cầm trịch thiết kế công nghệ.
    *   *Nhiệm vụ:* Thiết kế ERD, API, chọn Tech Stack. Tạo các bản mẫu (Prototype) ở đầu mỗi vòng xoắn ốc để đánh giá rủi ro (Ví dụ: Test thử API ElevenLabs xem có bị lệch timestamp không).

### B. Nhóm Thực thi (The Scrum Team)
Tập trung vào các Sprint của Agile (Kỹ thuật, Code & Test).

*   **3. Scrum Master (Người điều phối Agile):**
    *   *Vai trò:* "Bảo vệ" quy trình làm việc.
    *   *Nhiệm vụ:* Đảm bảo các buổi họp (Daily Standup, Sprint Planning) diễn ra đúng giờ. Loại bỏ các trở ngại (Blockers) cho team Dev.
*   **4. Đội ngũ Lập trình (Development Team):**
    *   **Backend Developer(s) (FastAPI/Python):** Xây dựng API, quản lý Database, viết Worker Celery xử lý AI.
    *   **Frontend Mobile Developer(s) (Flutter):** Viết app cho User (Smart Player, DRM, Wallet).
    *   **Frontend Web Developer(s) (Flet/React):** Viết Creator Studio và Admin Dashboard.
*   **5. Quality Assurance (QA - Kỹ sư Kiểm thử):**
    *   *Vai trò:* Người gác cổng chất lượng.
    *   *Nhiệm vụ:* Viết Test Case dựa trên Tiêu chí nghiệm thu (Acceptance Criteria). Test liên tục ngay trong Sprint thay vì đợi cuối dự án. Kiểm tra các "Sad Path" (Mất mạng, lỗi thẻ).

## 3. Quy trình làm việc thực tế (The Workflow in Action)

### Vòng xoắn ốc 1: Nền tảng cốt lõi (Core Foundation)
*   **Kế hoạch & Phân tích rủi ro:** Architect làm PoC xác thực việc kết nối FastAPI và PostgreSQL có mượt không.
*   **Thực thi (Agile):**
    *   *Sprint 1:* Dev Backend làm Auth (Đăng nhập/Đăng ký) và CRUD cho Users, Books. QA test API.
    *   *Sprint 2:* Dev Mobile làm giao diện Home, Login. Nối API. PO nghiệm thu màn hình Home.

### Vòng xoắn ốc 2: Tính năng khó - Đồng bộ AI (The Sync Challenge)
*   **Kế hoạch & Phân tích rủi ro:** Architect test rủi ro của tính năng Highlight Text và Manual Page Turn. Làm 1 Prototype nhỏ trên Flutter để xem độ trễ âm thanh.
*   **Thực thi (Agile):**
    *   *Sprint 3:* Dev Backend tích hợp ElevenLabs API, lưu metadata tọa độ.
    *   *Sprint 4:* Dev Mobile làm Smart Player, đọc file JSON và highlight text. QA test độ trễ (<100ms).

### Vòng xoắn ốc 3: Tài chính & Phát hành (Finance & Release)
*   **Kế hoạch & Phân tích rủi ro:** Đánh giá rủi ro trừ sai tiền ví (Wallet). Áp dụng Database Transaction.
*   **Thực thi (Agile):**
    *   *Sprint 5:* Backend làm tính năng Trừ tiền, sinh Transaction & Ledger. QA test cực gắt kịch bản mất mạng.
    *   *Sprint 6:* Hoàn thiện UI/UX. Chuẩn bị UAT (User Acceptance Testing) để phát hành bản Alpha.

---
*Lưu ý: Mô hình này giúp team không bị "ngợp" bởi khối lượng tính năng. Rủi ro khó nhất luôn được Architect xử lý trước khi Dev bắt tay vào code.*

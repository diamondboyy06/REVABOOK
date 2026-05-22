# BÁO CÁO RÀ SOÁT TỔNG THỂ DỰ ÁN REVABOOK (SOLUTION ARCHITECT REVIEW REPORT)

Đánh giá dựa trên tài liệu: Ý tưởng cốt lõi, Sơ đồ tính năng (Feature Map), Sơ đồ dữ liệu (ERD & DB Design) đã được xây dựng trước đó.

---

## 🔴 CỜ ĐỎ (RED FLAGS) - Các vấn đề nghiêm trọng cần họp và giải quyết ngay

### 1. Nút thắt hiệu năng: Chắp vá âm thanh (AI Chat Correction)
*   **Vấn đề (Tính khả thi):** Tính năng "AI Chat Agent sửa lỗi cục bộ" (chỉ render lại 3 giây audio bị lỗi rồi lưu đè). Thực tế, các mô hình TTS hiện tại (như ElevenLabs) thay đổi ngữ điệu (intonation) rất nhiều dựa trên ngữ cảnh xung quanh. Nếu ta chỉ cắt/ghép 3 giây mới vào giữa 1 đoạn audio cũ, chỗ nối âm thanh sẽ bị "khớp" và nghe rất giả tạo.
*   **Hành động:** BA & PO cần xác định lại. Kỹ thuật đề xuất: Khi sửa, AI phải sinh lại (re-generate) *toàn bộ câu* chứa lỗi đó, thay vì chỉ 1 từ hay vài giây, sau đó hệ thống mới ghi đè file audio của câu đó vào playlist.

### 2. Xử lý Offline Mode & DRM trên Flutter
*   **Vấn đề (Tính toàn vẹn & Khả năng kiểm thử):** Tải sách về đọc Offline (có mã hóa DRM). Việc giải mã (decrypt) file audio và hình ảnh on-the-fly (ngay trong lúc chạy) trên Flutter rất tốn tài nguyên CPU, dễ gây giật lag hoặc crash app trên các thiết bị yếu.
*   **Hành động:** Kỹ thuật cần làm một bài Proof of Concept (PoC) nhỏ để test hiệu năng giải mã thư viện DRM trên Flutter trước khi đưa vào code chính thức. Phải bổ sung kịch bản: *Nếu máy quá yếu, DRM giải mã không kịp dòng chảy audio thì app xử lý sao?*

### 3. Thiếu cơ chế theo dõi tiến trình AI (Async Task Tracking)
*   **Vấn đề (Tính nhất quán DB):** Trong `REVABOOK_DB_DESIGN.md`, tôi thiết kế bảng `books` và `chapters` nhưng chưa có bảng nào theo dõi trạng thái tiến trình dịch thuật/lồng tiếng hàng loạt (Celery Task).
*   **Hành động:** Thêm ngay một bảng `system_tasks (id, reference_id, task_type, status, progress, error_logs)` để Creator có thể biết tiến trình render AI đang ở 10%, 50% hay đã FAILED do lỗi mạng.

---

## 🟡 CỜ VÀNG (YELLOW FLAGS) - Rủi ro tiềm ẩn & Cần làm rõ

### 1. Đồng bộ Word-level Timestamp (Highlight sách chữ)
*   **Vấn đề (Tính khả thi API):** Để làm text sáng lên chuẩn xác từng từ/câu, API của OpenAI TTS hoặc ElevenLabs phải hỗ trợ trả về `word-level timestamps`. Nếu mô hình không hỗ trợ tốt (đặc biệt với các ngôn ngữ hiếm), tính năng Highlight sẽ bị lệch pha.
*   **Tinh chỉnh:** Chỉ nên cam kết (Acceptance Criteria) đồng bộ ở mức độ **CÂU (Sentence-level)** thay vì mức độ **TỪ (Word-level)** để đảm bảo an toàn kỹ thuật.

### 2. Giao dịch Wallet & Kịch bản mất mạng (Edge Cases)
*   **Vấn đề (Tính toàn vẹn):** User bấm "Mua sách", Backend đã trừ tiền trong `users.wallet_balance` nhưng lúc `INSERT` vào bảng `user_libraries` thì database sập hoặc lỗi mạng. User mất tiền nhưng không có sách.
*   **Tinh chỉnh:** Bắt buộc áp dụng cơ chế **Database Transaction (BEGIN - COMMIT - ROLLBACK)** ở tầng Backend API. Nếu bất kỳ bước nào thất bại, tiền phải được hoàn về lập tức.

### 3. Thiếu Tiêu chí Nghiệm thu cụ thể (Testability)
*   **Vấn đề:** Các tính năng trong Feature Map đang mô tả dưới dạng định tính (ví dụ: "Highlight đồng bộ theo giọng đọc"). QA không thể viết test case nếu không có con số.
*   **Tinh chỉnh:** Thêm các chỉ số như: *Độ trễ tối đa giữa audio và highlight là < 100ms*, *Thời gian bắt đầu phát audio sau khi bấm Play không vượt quá 2 giây*.

---

## 🟢 ĐỀ XUẤT TỐI ƯU (GREEN ENHANCEMENTS) - Chuẩn bị cho giai đoạn Code

### 1. Đề xuất Kiến trúc Giao tiếp (API Design)
Để giải quyết bài toán giao tiếp giữa Mobile App/Creator Studio và Backend, tôi đề xuất thiết kế API theo 3 giao thức:
*   **RESTful API (JSON):** Dùng cho các thao tác CRUD truyền thống (Đăng nhập, Lấy danh sách sách, Lịch sử giao dịch, Lấy token DRM).
*   **Server-Sent Events (SSE) hoặc WebSockets:** Bắt buộc dùng cho Creator Studio. Khi AI tiến hành dịch và lồng tiếng (mất hàng giờ), Backend sẽ dùng SSE để đẩy phần trăm (progress) về liên tục cho Frontend hiển thị thanh tiến trình mà không cần Client phải F5 hay ping liên tục (Polling).
*   **HLS (HTTP Live Streaming):** Phục vụ luồng Smart Player, băm nhỏ file audio thành các đoạn 10 giây (`.ts`) để truyền tải, gắn kèm AES-128 encryption cho mục đích DRM.

### 2. Đề xuất Cải tiến Cơ sở dữ liệu (Database Enhancement)
*   **Bổ sung Audit Trail:** Để đối soát tài chính vững chắc, cần thêm bảng `wallet_ledgers (id, user_id, amount_change, balance_after, reason, created_at)`. Bảng này có đặc tính *Append-Only* (chỉ thêm, không sửa xóa) để truy vết mọi biến động số dư.
*   **Tối ưu Storage:** Phân tách rõ ràng giữa `raw_content` (dữ liệu thô của Tác giả upload - lưu ở S3 Standard) và `processed_content` (dữ liệu đã lồng tiếng, tối ưu dung lượng - lưu ở S3 CDN Edge) để giảm thiểu chi phí băng thông egress.

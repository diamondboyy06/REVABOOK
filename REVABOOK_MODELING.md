# MÔ HÌNH HÓA DỰ ÁN REVABOOK (PROJECT MODELING)

## 1. Sơ đồ luồng dữ liệu (Data Flow)

1.  **Tác giả** -> Upload (Text/Comic) -> **Backend Server**.
2.  **Backend** -> Chuyển vào **Task Queue (Celery/Redis)** -> **AI Engine** xử lý (Dịch thuật nguyên cuốn / OCR / NLP / TTS).
3.  **AI Engine** -> Lưu Audio (đa ngôn ngữ) vào **Storage (S3)** & Metadata vào **Database** (Lưu kết quả vĩnh viễn để tái sử dụng).
4.  **Độc giả** -> Request -> **Backend** (Kiểm tra DRM/Thanh toán) -> **CDN/HLS Streaming**.
5.  **Feedback Loop:** Độc giả -> Báo lỗi Text/Audio -> **Database (Report)** -> Chủ quản dùng **AI Chat Agent** -> Sửa đổi cục bộ (Update DB/S3).

## 2. Các Modules chính (System Components)

### A. Mobile App (Flutter)
- **Content Discovery:** Home, Search, Category (Hỗ trợ đa ngôn ngữ).
- **Smart Media Player:** HLS Streaming, Background Playback.
    - Sách chữ: Text Highlighting đồng bộ audio.
    - Truyện tranh: Manual Page Turn (lật trang thủ công) kết hợp Audio Sync.
- **Offline Mode:** Tải sách đã mã hóa về máy.
- **Feedback System:** Công cụ bôi đen/chọn đoạn để gửi báo cáo lỗi.

### B. Admin/Creator Studio (Flet / React Web)
- **Workflow Manager:** Kéo thả kịch bản, quản lý tiến trình Dịch thuật & Lồng tiếng hàng loạt.
- **AI Correction Agent (Chatbot):** Giao diện Chat nội bộ để chủ quản ra lệnh cho AI sửa lỗi (dịch lại, đổi giọng) dựa trên report của người dùng.
- **Analytics:** Biểu đồ doanh thu, lượt nghe, tỷ lệ lỗi (Error tracking).

### C. Backend & Infrastructure
- **API Gateway (FastAPI):** Xử lý request, Auth, Payment.
- **Worker Service:** Xử lý tác vụ AI nặng một cách bất đồng bộ.
- **Storage:** AWS S3 hoặc MinIO (Lưu trữ file audio/ảnh có mã hóa).

## 3. Cấu trúc Dữ liệu (Polyglot Persistence)

- **Relational DB (PostgreSQL):** Quản lý User, Wallet, Transaction, DRM Keys, Error Reports.
- **Document DB (MongoDB):** Lưu kịch bản đa ngôn ngữ (Translated Script), tọa độ bong bóng thoại (Coordinates Mapping), metadata của sách.
- **Cache (Redis):** Session, Task Queue, Rate limiting.

## 4. Mô hình đồng bộ Text & Audio (Sync Model)
- **Truyện tranh (Coordinate Mapping):** Mỗi "Bong bóng thoại" được định vị bằng tọa độ (x, y, width, height). App sẽ highlight tọa độ tương ứng với timestamp của audio. Audio dừng khi người dùng chưa lật trang tiếp theo.
- **Sách chữ (Text-Audio Alignment):** Lưu trữ dạng file JSON/VTT chứa cặp `{ text_block, start_time, end_time }`. App sẽ highlight `text_block` (câu/đoạn) khi trình phát nhạc đạt đến `start_time`.

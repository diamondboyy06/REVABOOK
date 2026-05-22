# QUY TRÌNH PHÁT TRIỂN DỰ ÁN (AI WORKFLOW) & STRICT AI RULES

Tài liệu này định nghĩa quy trình tương tác và các **QUY TẮC CỨNG (HARD RULES)** buộc AI phải tuân thủ nghiêm ngặt trong suốt vòng đời dự án REVABOOK. Việc tuân thủ tài liệu này là ưu tiên số 1 của AI.

---

## PHẦN 1: QUY TẮC BẮT BUỘC CHO AI (STRICT AI RULES)

Để đảm bảo dự án vận hành đúng mô hình **Spiral-Agile Hybrid** và không xảy ra rủi ro hệ thống, AI **BẮT BUỘC** phải tuân thủ các quy tắc sau trước khi thực hiện bất kỳ hành động nào:

1.  **KHÔNG NHẢY CÓC (No Skipping Steps):** Tuyệt đối không tự ý viết code (Bước 4) khi chưa hoàn thành Bước 2 (Kiểm tra khả thi) và chưa được Coder cấp phép ở Bước 3 ("Chốt" / "Tiến hành"). Mọi yêu cầu tính năng mới đều phải bắt đầu từ Bước 1.
2.  **LUÔN ĐÁNH GIÁ RỦI RO (Spiral Model Compliance):** Đối với các tính năng phức tạp (liên quan đến Audio, AI, Sync, Thanh toán), AI đóng vai trò Solution Architect **phải** yêu cầu và thực hiện bản mẫu (Proof of Concept - PoC) để kiểm chứng rủi ro trước khi đưa vào Sprint code chính thức.
3.  **TƯ DUY AGILE (Sprint Focus):** Xử lý công việc theo từng khối nhỏ (Sprint). Code xong phần nào phải đảm bảo phần đó có thể chạy và kiểm thử được.
4.  **BẢO VỆ KIẾN TRÚC & DỮ LIỆU:** Bất kỳ thay đổi nào về luồng logic phải được đối chiếu chéo với các file:
    *   `REVABOOK_DB_DESIGN.md` (Không tự ý đổi cấu trúc DB nếu chưa thảo luận).
    *   `REVABOOK_TEAM_WORKFLOW.md` (Xác định rõ task này thuộc về Frontend, Backend hay AI Engine).
    *   `REVABOOK_MODELING.md` và `REVABOOK_FEATURE_MAP.md`.
5.  **GHI LOG BẮT BUỘC:** Mọi thay đổi lớn về code, kiến trúc hoặc chốt tính năng đều **phải** được ghi nhận vào file `AI_LOG.md`.

---

## PHẦN 2: QUY TRÌNH 6 BƯỚC TIÊU CHUẨN

AI và Coder sẽ tương tác tuần tự theo vòng lặp sau:

### Bước 1: Tiếp nhận Ý tưởng (Idea Gathering)
- AI lắng nghe ý tưởng, yêu cầu hoặc vấn đề từ Coder.
- Trích xuất thông tin, đối chiếu với `REVABOOK_FEATURE_MAP.md`. Không tự ý thực hiện thay đổi lớn khi chưa hiểu rõ mục đích.

### Bước 2: Kiểm tra Tính khả thi & Phản hồi (Feasibility Check - The Spiral)
- AI (vai trò Architect) phân tích yêu cầu dựa trên Tech Stack.
- Phân tích rủi ro kỹ thuật (Bottlenecks, Edge cases).
- Đưa ra phản hồi về ưu/nhược điểm và đề xuất giải pháp tối ưu. Nếu rủi ro cao, đề xuất làm Prototype/PoC.

### Bước 3: Thảo luận & Chốt phương án (Iteration & Confirmation)
- Tiếp tục nhận ý kiến phản hồi từ Coder để điều chỉnh giải pháp.
- Chỉ chuyển sang bước tiếp theo khi Coder xác nhận rõ ràng: **"Chốt"**, **"Tiến hành"**, hoặc **"Đồng ý"**.

### Bước 4: Lập trình & Kiểm tra lỗi (Implementation & Debugging - The Agile Sprint)
- AI tiến hành viết code cho tính năng đã chốt.
- Đảm bảo tuân thủ thiết kế Database (PostgreSQL) và giao thức (FastAPI/Flutter).
- Tự kiểm tra lỗi (self-debug), tối ưu hóa code.

### Bước 5: Trả kết quả (Delivery)
- Trình bày code rõ ràng, giải thích các thành phần chính.
- Hướng dẫn Coder cách tích hợp, chạy thử và kiểm thử (Acceptance Criteria).

### Bước 6: Tiếp nhận phản hồi & Lặp lại (Feedback Loop)
- Chờ Coder kiểm tra kết quả thực tế trên máy Local. Nhận Feedback và quay lại Bước 1 để hoàn thiện tính năng hoặc bắt đầu Sprint mới.
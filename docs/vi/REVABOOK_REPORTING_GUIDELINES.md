# QUY TẮC & BIỂU MẪU BÁO CÁO CÔNG VIỆC (REPORTING GUIDELINES)

Tài liệu này quy định các biểu mẫu (Templates) và tiêu chuẩn báo cáo bắt buộc dành cho các thành viên trong dự án REVABOOK. Việc ghi chép này giúp AI và toàn bộ đội ngũ dễ dàng theo dõi tiến độ (tracking), kiểm soát rủi ro và đánh giá hiệu suất sau mỗi Sprint/Vòng xoắn ốc.

Mỗi khi một Sprint hoặc một Vòng xoắn ốc (Spiral Phase) kết thúc, các nhân sự phụ trách bắt buộc phải tạo/cập nhật file Markdown báo cáo tương ứng trong thư mục `docs/reports/` (Ví dụ: `docs/reports/Sprint_1_Report.md`).

---

## 1. Biểu mẫu Báo cáo của Product Owner (PO)
**Thời điểm báo cáo:** Cuối mỗi Sprint (Sprint Review) & Cuối Vòng xoắn ốc.
**Mục đích:** Đánh giá xem phần mềm đã đáp ứng đúng nhu cầu kinh doanh chưa.

```markdown
### [PO REPORT] Tóm tắt Nghiệm thu Sprint [Số Sprint]
* **Ngày nghiệm thu:** YYYY-MM-DD
* **Tính năng đã yêu cầu (Sprint Backlog):** [Liệt kê các tính năng]
* **Kết quả Nghiệm thu (Accepted/Rejected):**
  * Tính năng A: [Accepted] - Lý do: Chạy mượt, đúng thiết kế.
  * Tính năng B: [Rejected] - Lý do: UX chưa tốt, còn lỗi khi mất mạng.
* **Thay đổi định hướng (Nêu rõ nếu có thay đổi cho Sprint tới):** ...
```

---

## 2. Biểu mẫu Báo cáo của Solution Architect
**Thời điểm báo cáo:** Bắt đầu và Kết thúc Vòng xoắn ốc (Giai đoạn Phân tích rủi ro & Làm PoC).
**Mục đích:** Đánh giá rủi ro kỹ thuật và chốt hướng đi công nghệ.

```markdown
### [ARCHITECT REPORT] Đánh giá Rủi ro Vòng xoắn ốc [Số]
* **Ngày đánh giá:** YYYY-MM-DD
* **Rủi ro cốt lõi đang xử lý:** [VD: Tốc độ load audio chậm, chi phí API cao]
* **Kết quả Proof of Concept (PoC):**
  * Phương án A: [Thất bại] - Quá tải CPU.
  * Phương án B: [Thành công] - Tối ưu 30% chi phí.
* **Quyết định Kỹ thuật (Tech Decision):** [Ghi rõ kiến trúc sẽ áp dụng cho team Dev code]
* **Cập nhật DB/API (Có/Không):** [Liệt kê các file thiết kế đã bị thay đổi]
```

---

## 3. Biểu mẫu Báo cáo của Scrum Master
**Thời điểm báo cáo:** Kết thúc Sprint (Sprint Retrospective).
**Mục đích:** Đánh giá hiệu suất làm việc của team và các vật cản (blockers).

```markdown
### [SCRUM MASTER REPORT] Tổng kết Sprint [Số]
* **Ngày tổng kết:** YYYY-MM-DD
* **Mục tiêu Sprint (Sprint Goal):** [Đạt / Không đạt]
* **Các vấn đề đã cản trở team (Blockers):** [VD: Mất 2 ngày chờ API key từ đối tác]
* **Điểm tốt cần phát huy (What went well):** ...
* **Điểm cần cải thiện (What to improve):** ...
* **Hành động cho Sprint tới (Action Items):** ...
```

---

## 4. Biểu mẫu Báo cáo của Đội ngũ Lập trình (Dev Team)
**Thời điểm báo cáo:** Hoàn thành một Task/Tính năng hoặc cuối Sprint.
**Mục đích:** Báo cáo chi tiết về code, các thư viện đã dùng và API đã hoàn thiện.

```markdown
### [DEV REPORT] Báo cáo Kỹ thuật - [Tên Tính năng / Task]
* **Người thực hiện:** [Backend / Frontend Mobile / Frontend Web]
* **Ngày hoàn thành:** YYYY-MM-DD
* **Tóm tắt công việc:** [VD: Hoàn thành API Login, Tích hợp Stripe]
* **Pull Request / Commit Link:** [Link PR]
* **Thư viện / Packages mới được thêm vào:** [VD: `flutter_stripe`, `celery`]
* **Nợ kỹ thuật (Technical Debt - Nếu có):** [VD: "Code phần xử lý Audio đang hardcode, cần refactor ở Sprint sau"]
```

---

## 5. Biểu mẫu Báo cáo của Quality Assurance (QA)
**Thời điểm báo cáo:** Xuyên suốt Sprint (Ngay khi Dev báo xong 1 task).
**Mục đích:** Trình bày kết quả kiểm thử và danh sách lỗi.

```markdown
### [QA REPORT] Báo cáo Kiểm thử - [Tên Tính năng]
* **Ngày test:** YYYY-MM-DD
* **Môi trường Test:** [Local / Staging / iOS 16 / Android 13]
* **Tỷ lệ Pass (Pass Rate):** [VD: 8/10 Test cases Passed]
* **Danh sách Lỗi (Bugs / Red Flags):**
  * Bug 1: [Mức độ: Critical] - App crash khi nhấn đúp nút Thanh toán.
  * Bug 2: [Mức độ: Minor] - Nút bấm bị lệch 2px trên màn hình nhỏ.
* **Đề xuất (Có cho phép Release không?):** [Yes / No - Yêu cầu fix Bug 1 ngay lập tức]
```

---

## 🎯 QUY TẮC TUÂN THỦ (COMPLIANCE RULE)
**Bất kỳ AI hoặc con người nào** khi đóng vai trò là một trong 5 thành viên trên để thực hiện việc ghi chú tiến độ dự án, **BẮT BUỘC** phải sao chép đúng định dạng biểu mẫu này và điền thông tin vào. Không tự ý sáng tạo biểu mẫu mới để đảm bảo hệ thống Log/Tracking đồng nhất.

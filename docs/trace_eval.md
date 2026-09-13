# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Đinh Tiến Cảnh  
> **Mã Sinh Viên / Mã Học viên:** 2A202602918  
> **Chủ đề Lựa chọn:** Trợ lý Học vụ & Tra cứu Lịch thi VinUni 

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** |4 / 5 | Cần thực hiện chuỗi suy luận logic tuần tự: Xác thực danh tính sinh viên $\rightarrow$ Tra cứu tiến độ học tập / GPA $\rightarrow$ Kiểm tra danh tính Cố vấn học tập (Academic Advisor) tương ứng $\rightarrow$ Đối chiếu lịch trống $\rightarrow$ Xác nhận và ghi nhận lịch hẹn tư vấn. |
| **2. Tool Interaction** |5 / 5 | Phụ thuộc trực tiếp vào các nguồn dữ liệu ngoài qua MCP/API: Hệ thống Quản lý Đào tạo (SIS) để đọc GPA/học bạ, Hệ thống Quản lý Khảo thí để lấy lịch thi/phòng thi, và Dịch vụ Lịch (Calendar Service) để tra cứu khung giờ trống và đặt lịch hẹn. |
| **3. Dynamic Decision** |4 / 5 | Bước tiếp theo thay đổi linh hoạt theo ngữ cảnh quan sát (Observation): Nếu sinh viên có môn thi bị trùng giờ thì chuyển hướng cảnh báo; nếu Cố vấn phụ trách kín lịch thì gợi ý khung giờ khác hoặc liên hệ bộ phận hỗ trợ dự phòng; nếu điểm môn nào dưới chuẩn thì chủ động gợi ý lịch tư vấn cải thiện điểm. |
| **4. Long Horizon Goal** |3 / 5 | Mục tiêu bám sát một phiên hỗ trợ trọn vẹn (giải quyết chu trình từ tra cứu điểm/lịch thi đến khi hoàn tất đặt lịch tư vấn). Độ dài phiên tương tác kéo dài từ 2 đến 4 bước hội thoại, duy trì trạng thái ngữ cảnh sinh viên xuyên suốt phiên làm việc. |
| **TỔNG ĐIỂM AGENTIC FIT** | **16 / 20** | *Tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "query": "Em là sinh viên SV2026001 đang gặp khó khăn trong việc chọn môn kỳ tới. Bạn xem cố vấn học tập của em là ai rồi đặt giúp em một lịch hẹn với thầy/cô đó vào 09:30 sáng thứ Sáu tuần này nhé.",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "academic_query",
    "arguments": {
      "student_id": "SV2026001"
    },
    "observation": {
      "status": "SUCCESS",
      "student_id": "SV2026001",
      "data": {
        "full_name": "Nguyễn Văn An",
        "class": "AI-K4",
        "gpa": 3.85,
        "email": "an.nv@vinuni.edu.vn",
        "status": "Đang học",
        "advisor": "PGS.TS Nguyễn Văn A"
      }
    },
    "latency_ms": 7028.39
  },
  {
    "step": 2,
    "query": "Em là sinh viên SV2026001 đang gặp khó khăn trong việc chọn môn kỳ tới. Bạn xem cố vấn học tập của em là ai rồi đặt giúp em một lịch hẹn với thầy/cô đó vào 09:30 sáng thứ Sáu tuần này nhé.",
    "action_type": "TOOL_EXECUTION",
    "tool_name": "schedule_appointment",
    "arguments": {
      "student_id": "SV2026001",
      "advisor_name": "PGS.TS Nguyễn Văn A",
      "datetime_str": "09:30 25/10/2024"
    },
    "observation": {
      "status": "SUCCESS",
      "booking_id": "BK-SV2026001-99",
      "student_id": "SV2026001",
      "datetime": "09:30 25/10/2024",
      "advisor": "PGS.TS Nguyễn Văn A",
      "message": "Đặt lịch thành công cho sinh viên SV2026001 với PGS.TS Nguyễn Văn A vào lúc 09:30 25/10/2024."
    },
    "latency_ms": 3363.52
  },
  {
    "step": 3,
    "query": "Em là sinh viên SV2026001 đang gặp khó khăn trong việc chọn môn kỳ tới. Bạn xem cố vấn học tập của em là ai rồi đặt giúp em một lịch hẹn với thầy/cô đó vào 09:30 sáng thứ Sáu tuần này nhé.",
    "action_type": "FINAL_ANSWER",
    "thought": "Gemini phản hồi trực tiếp bằng văn bản (không cần gọi công cụ).",
    "output": "Chào bạn Nguyễn Văn An,\n\nTôi đã hoàn tất việc hỗ trợ bạn. Dưới đây là thông tin chi tiết:\n1. Cố vấn học tập của bạn: PGS.TS Nguyễn Văn A.\n2. Kết quả đặt lịch: Lịch hẹn tư vấn học vụ của bạn đã được đặt thành công (09:30 thứ Sáu, Mã đặt lịch: BK-SV2026001-99).",
    "latency_ms": 5257.94
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [x] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** 5 / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** 6 lượt.
- **Kết quả đẩy Repo nộp bài:** [x] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!


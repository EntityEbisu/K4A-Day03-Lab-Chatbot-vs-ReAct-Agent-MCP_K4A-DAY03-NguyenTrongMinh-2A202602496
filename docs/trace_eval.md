# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Nguyen Trong Minh
> **Mã Sinh Viên / Mã Học viên:** 2A202602496
> **Chủ đề Lựa chọn:** 1.1 Trợ lý Học vụ & Tra cứu Lịch thi VinUni (Tra cứu điểm GPA, lịch thi và đặt lịch tư vấn học vụ với Cố vấn)

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | 4 / 5 | Bài toán yêu cầu suy luận đa bước rõ rệt: TC04 phải tra cứu `academic_query` để lấy tên cố vấn trước, sau đó mới gọi `schedule_appointment`. Ngay cả TC03 đơn bước vẫn cần trích xuất 3 tham số (student_id, datetime, advisor) và validate trước khi gọi tool. Không phải FAQ một bước. |
| **2. Tool Interaction** | 5 / 5 | Bắt buộc kết nối MCP Server để lấy dữ liệu thời gian thực (GPA, email, advisor, booking_id). LLM không thể trả lời chính xác nếu thiếu `academic_query`/`schedule_appointment` qua JSON-RPC 2.0; hallucination sẽ xảy ra nếu chỉ dùng kiến thức tĩnh. |
| **3. Dynamic Decision** | 4 / 5 | Bước tiếp theo phụ thuộc hoàn toàn vào Observation: nếu `academic_query` trả về SUCCESS thì đặt lịch với advisor tương ứng; nếu NOT_FOUND (TC05 - SV9999999) thì dừng và trả lời lịch sự thay vì gọi tiếp. Decision phân nhánh theo kết quả tool. |
| **4. Long Horizon Goal** | 3 / 5 | Cần giữ mục tiêu xuyên suốt 2-3 lượt ReAct (ví dụ: "đặt lịch cho SV2026002 vào 20/09" phải nhớ cả student_id, datetime và advisor đã tra cứu). Horizon ngắn-trung bình, chưa đến mức multi-session memory nhưng vượt quá chat một lượt. |
| **TỔNG ĐIỂM AGENTIC FIT** | **16 / 20** | *Nếu tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System. => 16/20: Khuyến nghị ReAct Agent + MCP, không dùng Chatbot thuần túy.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
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
        "gpa": 3.85
      }
    },
    "latency_ms": 120.5
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [ ] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** ___ / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** ___ lượt.
- **Kết quả đẩy Repo nộp bài:** [ ] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

> ✅ **HOÀN TẤT NỘP BÀI:** Sao chép đường link GitHub Repository cá nhân của bạn và dán vào ô nộp bài trên hệ thống LMS VLearn để hoàn tất Bài Lab 3!

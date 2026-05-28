# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> *Câu trả lời của bạn*

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Câu trả lời của bạn*

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *Câu trả lời của bạn*

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *Câu trả lời của bạn*

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)

1. Khi nào Streaming quan trọng nhất?
    Streaming tỏa sáng trong các tình huống yêu cầu phản hồi ngay lập tức hoặc khi làm việc với dữ liệu vô hạn không bao giờ dừng lại.

        - Tối ưu hóa trải nghiệm người dùng (UX) thời gian thực: Trong các ứng dụng AI như ChatGPT hay Gemini, việc tạo văn bản (text generation) mất thời gian. Nếu không có streaming, bạn sẽ phải nhìn màn hình chờ hàng chục giây. Streaming trả về từng "token" ngay khi nó được tạo ra, giúp bạn có thể bắt đầu đọc ngay lập tức.

        - Truyền tải nội dung đa phương tiện: Khi nghe nhạc hay xem phim, bạn không cần phải tải toàn bộ file video dung lượng cao về máy. Hệ thống chia nhỏ dữ liệu và phát tới đâu tải tới đó (ví dụ: YouTube, Spotify).

        - Xử lý dữ liệu thời gian thực (Real-time Analytics): Trong kỹ thuật dữ liệu (Data Engineering), streaming bắt buộc phải dùng cho các hệ thống giám sát cảnh báo:

            + Phát hiện giao dịch gian lận ngân hàng ngay trong tích tắc (trước khi thẻ bị trừ tiền).

            + Phân tích dữ liệu từ hàng ngàn cảm biến IoT (Internet of Things) để dự báo hỏng hóc máy móc tức thời.

2. Khi nào Non-streaming lại phù hợp hơn?
    Non-streaming (thường được gọi là Batch Processing trong xử lý dữ liệu, hoặc Caching/Download toàn bộ) là lựa chọn tối ưu khi bạn cần tính toàn vẹn của cấu trúc dữ liệu hoặc khi tối ưu hóa chi phí/tài nguyên.

        - Yêu cầu tính toàn vẹn cấu trúc (Strict Formatting): Trong lập trình AI, nếu bạn gọi API của một mô hình ngôn ngữ lớn để trả về một định dạng dữ liệu nghiêm ngặt như JSON, bạn buộc phải dùng non-streaming. Hệ thống cần đợi toàn bộ chuỗi JSON được tạo xong và đóng ngoặc hợp lệ { ... } thì mới có thể phân tích cú pháp (parse) thành công.

        - Xử lý dữ liệu lớn và phức tạp (Batch Processing): Khi bạn cần thực hiện các phép toán trên toàn bộ tập dữ liệu (ví dụ: huấn luyện mô hình Machine Learning, tính tổng doanh thu cuối tháng, hoặc sắp xếp toàn bộ cơ sở dữ liệu), bạn phải thu thập đủ dữ liệu trước rồi mới xử lý cùng một lúc.

        - Tối ưu hóa tài nguyên mạng: Các kết nối streaming đòi hỏi máy chủ và máy khách phải duy trì một kết nối mở liên tục (persistent connection). Đối với các tác vụ chạy ngầm (background jobs) hoặc khi mạng chập chờn, việc gửi một request và đợi nhận lại toàn bộ kết quả (một lần duy nhất) sẽ ổn định và tiết kiệm tài nguyên máy chủ hơn.

## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 

# Bằng chứng Day 22 — Lê Hoàng Thiên Phú

## Kết quả V1 so với V2

Cả hai prompt được đánh giá trên 50 cặp QA bằng cùng knowledge base, retriever top-3 và bốn chỉ số RAGAS. Số liệu dưới đây lấy từ `03_ragas_report.json`, khớp ảnh `03_ragas_scores.png`.

| Chỉ số | V1 | V2 |
|---|---:|---:|
| faithfulness | 0.945325 | 0.943166 |
| answer_relevancy | 0.909866 | 0.892749 |
| context_recall | 1.000000 | 1.000000 |
| context_precision | 0.945000 | 0.945000 |

V1 có faithfulness cao hơn khoảng 0,00216 và answer relevancy cao hơn khoảng 0,01712. V1 yêu cầu trả lời ngắn 2–4 câu, chỉ dựa vào context và thừa nhận khi thiếu thông tin. Một giả thuyết là câu trả lời ngắn làm giảm phát biểu bổ sung và tập trung hơn vào câu hỏi. V2 yêu cầu phân tích, trả lời có tổ chức trong 3–5 câu; phần diễn giải dài hơn có thể làm giảm nhẹ độ liên quan. Đây là giải thích có thể có, không phải kết luận nhân quả: một lần chạy và điểm tổng hợp chưa đủ để chứng minh nguyên nhân hoặc ý nghĩa thống kê.

Cả hai phiên bản đạt faithfulness ≥ 0,9. Context recall bằng 1,0 ở cả hai, context precision gần bằng 0,945 (chênh lệch khoảng 10^-12, xem như hòa). Hai prompt dùng cùng cơ chế truy xuất nên kết quả retrieval gần nhau là hợp lý. Trên lần đánh giá này, V1 là lựa chọn ưu tiên nếu mục tiêu là câu trả lời ngắn và liên quan; chưa có số đo latency/token riêng cho từng phiên bản để kết luận về hiệu suất hoặc chi phí.

## Danh mục bằng chứng

- `01_langsmith_traces.png`: dashboard ghi nhận 100 traces, error rate 0% tại thời điểm chụp.
- `01_langsmith_50_traces.png`: dashboard sau bước 1 ghi nhận 50 traces.
- `02_prompt_hub.png`: hai prompt trên Hub; xem `02_prompt_v1.png` và `02_prompt_v2.png` để đọc đầy đủ tên, nội dung và commit.
- `02_ab_routing_log.txt`: log thực tế push/pull Hub và 50 truy vấn, V1=19 và V2=31. Log có lỗi giải mã tiếng Việt từ PowerShell; giữ nguyên nội dung gốc, các nhãn routing và URL vẫn đọc được.
- `03_ragas_scores.png`, `03_ragas_report.json`: bảng so sánh và bản sao nguyên vẹn báo cáo RAGAS.
- `04_pii_demo_log.txt`, `04_json_demo_log.txt`: cùng một lần chạy demo gồm 6 case PII và 5 case JSON; cảnh báo export telemetry không ảnh hưởng kết quả validator.

## Đường dẫn project

[day22-lab trên LangSmith APAC](https://apac.smith.langchain.com/o/0ce76e9f-c1c7-4f55-8dd9-7e1af4a7d3d6/projects/p/30bcec2c-357f-470f-8392-d56cf63a2ff0)

Đây là URL workspace; chưa xác nhận truy cập công khai khi không đăng nhập. Cần kiểm tra chia sẻ trước khi yêu cầu điểm thưởng URL công khai và nộp URL trên LMS.

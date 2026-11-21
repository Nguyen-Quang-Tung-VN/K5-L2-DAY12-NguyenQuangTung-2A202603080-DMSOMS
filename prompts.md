# Khai báo dùng AI — Nguyễn Quang Tùng (2A202603080)

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity AI Assistant | Tóm tắt mục tiêu, quy tắc cốt lõi và lộ trình thực hiện bài lab Ngày 12 | Hiểu rõ bức tranh tổng thể và các mốc checkpoint cần đạt | Kiểm lại với file GUIDE.md và README.md trong repo |
| 2 | Antigravity AI Assistant | Làm rõ việc chọn 22 ảnh cốt lõi trong gói G10 khi thấy thư mục OMS có 20 ảnh | Nạp đúng 16 ảnh S01–S08 và 6 ảnh D01–D06 vào task CVAT | Kiểm lại số frame của task trên CVAT đủ đúng 22 ảnh |
| 3 | Antigravity AI Assistant | Kiểm tra các thuộc tính nhãn OMS trên cảnh S01, S02 theo quy chuẩn Guideline Cabin v1.0 | Phát hiện và khắc phục các điểm bẫy (ghế tính theo xe, SVIRO không có người thật trẻ em) | Chạy script cabin_check.py đạt 0 lỗi Checkpoint A |
| 4 | Antigravity AI Assistant | Hướng dẫn phân xử đối chiếu các dòng khác biệt trong file disagreement_log.csv | Điền chính xác các cột verdict, guideline_rule và action cho 17 dòng bất đồng | Đối chiếu từng quy tắc trong Guideline Cabin v1.0 |
| 5 | Antigravity AI Assistant | Gợi ý cấu trúc phân loại danh sách lớp v0 cho model DMS/OMS và câu hỏi leo thang | Hoàn thiện file class_list_v0.md và nhật ký ir_log.csv | Tự rà soát lại theo yêu cầu bài giảng slide 54 và RUBRIC.md |

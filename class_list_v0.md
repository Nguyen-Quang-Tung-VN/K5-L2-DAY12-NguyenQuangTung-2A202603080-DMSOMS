# Danh sách lớp v0 — Nguyễn Quang Tùng · G10

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_state` | open / closed / unknown | Phát hiện tài xế buồn ngủ (mắt nhắm liên tục > 1.5s) hoặc mất tập trung để phát cảnh báo âm thanh/rung vô lăng | Có, trừ khi bị đốm phản xạ LED NIR trên tròng kính che khuất |
| 2 | `gaze_zone` | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Theo dõi vùng chú ý của mắt; cảnh báo tài xế mất tập trung khi mắt rời khỏi mặt đường quá 2-3 giây | Có, phân tích hướng con ngươi và góc nghiêng mắt trên ảnh NIR |
| 3 | `head_pose` | yaw, pitch, roll (góc quay) | Ước lượng hướng quay đầu; phát hiện đầu gục xuống khi ngủ gật hoặc quay sang ghế phụ quá lâu | Có, thông qua 13 điểm mốc khuôn mặt (face13) |
| 4 | `phone_use` | held / mounted / lap | Phát hiện hành vi sử dụng điện thoại khi lái xe (gây xao nhãng nghiêm trọng và vi phạm luật an toàn giao thông) | Có khi thấy rõ đường viền, góc máy hoặc ánh sáng màn hình |
| 5 | `hand_on_wheel` | yes / no / unknown | Kiểm tra tài xế có đặt tay trên vô lăng hay không; bắt buộc cho tính năng tự lái L2/L3 khi yêu cầu tài xế sẵn sàng tiếp quản | Có, camera góc rộng nhìn bao quát vô lăng và vị trí tay |
| 6 | `yawn_detection` | yawn / normal / talking | Đếm tần suất ngáp để cảnh báo dấu hiệu mệt mỏi sớm trước khi tài xế thực sự nhắm mắt ngủ gật | Có, đo khoảng cách mở rộng giữa hai bờ môi qua điểm lip_upper và lip_lower |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `seat_occupancy` | empty / adult / child / object | Xác định trạng thái chiếm chỗ từng ghế; dùng để bật/tắt túi khí thông minh (tránh nổ túi khí ghế trống) và bật chuông nhắc thắt dây an toàn | Có, phân loại dựa trên hình khối và kích thước đối tượng |
| 2 | `seatbelt_status` | worn_correct / worn_incorrect / not_worn / unknown | Kiểm tra thắt dây an toàn đúng quy cách (dây chéo qua vai); cảnh báo nếu hành khách luồn dây dưới nách hoặc cài sau lưng | Có nếu dải dây có độ tương phản tốt với áo; khó thấy trên áo tối |
| 3 | `child_presence_detection` | infant_seat / child_seat / child | Hệ thống chống bỏ quên trẻ em trên xe (CPD) khi xe tắt máy và khóa cửa; kích hoạt còi/gửi thông báo về điện thoại phụ huynh | Có, nhận diện rõ cấu trúc hình học đặc thù của nôi/ghế an toàn |
| 4 | `left_behind_object` | bag / box / cup / other | Cảnh báo đồ vật để quên (ba lô, máy tính, túi xách, cốc nước) trước khi hành khách rời khỏi xe | Có với đồ vật kích thước trung bình và lớn |
| 5 | `passenger_posture` | upright / slouched / lying / out_of_position | Đánh giá tư thế ngồi của hành khách để điều chỉnh lực bung túi khí và vị trí đỡ bảo vệ tối ưu khi xảy ra va chạm | Có, phân tích bounding box thân người và hướng nghiêng cơ thể |
| 6 | `camera_blocked` | yes / no | Cảnh báo hệ thống an toàn khi camera khoang cabin bị che khuất bởi hành lý chất cao hoặc vật cản vô tình đè lên | Có, phát hiện toàn bộ hoặc phần lớn khung hình bị mất chi tiết/tối đen |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. **Câu hỏi:** Trong trường hợp trên ghế an toàn trẻ em có đặt một hình nộm thử nghiệm va chạm (child dummy/búp bê) như trong bộ SVIRO, hệ thống OMS nên phân loại đối tượng này là `object` (loại `other`) hay cần có một nhãn riêng là `dummy` để tránh gây nhiễu cho mô hình cảnh báo bỏ quên trẻ em (CPD)?
   - **Khung ví dụ:** `S02_rgb.png` (ghế giữa `rear_middle` có đặt chiếc ghế trẻ em kèm hình nộm mặc áo xanh).
   - **Bạn tạm gán thế nào và vì sao:** Tạm thời không gán `person` theo quy định tại mục 3 Guideline (*"Bộ ảnh không có trẻ em ngồi, thấy hình giống trẻ em thì báo coach, không gán person"*), mà chỉ gán box `child_seat` (thuộc tính `occupied = no`) để tránh dạy mô hình nhận nhầm búp bê/hình nộm là người thật.

2. **Câu hỏi:** Trên camera DMS sử dụng dải sóng cận hồng ngoại 940nm (NIR) vào ban đêm, tròng kính râm chống tia UV thường trở nên trong suốt, cho phép camera nhìn rõ mắt tài xế như kính trắng cận thị. Trong tình huống này, thuộc tính `glasses` nên ưu tiên gán là `sun` (theo loại kính thực tế tài xế đeo) hay `clear` (theo góc nhìn trực quan mà camera máy học ghi nhận được)?
   - **Khung ví dụ:** `D01.png` và `D03.png` (vùng mắt tài xế đeo kính dưới ánh sáng NIR).
   - **Bạn tạm gán thế nào và vì sao:** Tạm thời nếu nhìn rõ cả tròng kính và mắt bên trong thì gán `glasses = clear` (để mô hình biết mắt đang quan sát được xuyên qua kính), nếu tròng tối hẳn hoặc bị lóa phản xạ LED thì gán `unknown`. Đề xuất guideline làm rõ ưu tiên chức năng nhận dạng loại vật thể hay chức năng hỗ trợ theo dõi mắt.

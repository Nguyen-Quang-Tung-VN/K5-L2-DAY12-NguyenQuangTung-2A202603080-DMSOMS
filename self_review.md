# Tự đánh giá — Nguyễn Quang Tùng · G10

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S01_rgb.png` | `child_seat` (`rear_right`) & `person` (`rear_left`) | `ok` | Ghế gán đúng theo xe (bên trái ảnh là rear_right); seatbelt gán đúng not_worn. | Đã chuẩn |
| `S02_rgb.png` | Búp bê trẻ em ghế giữa `rear_middle` | `wrong_class` | Ban đầu gán nhầm là person; theo mục 3 SVIRO không có trẻ em ngồi nên đã xóa box person. | Đã sửa |
| `D01.png` | Mặt và mốc mắt tài xế | `missing` | Ban đầu thiếu skeleton face13; mặt rộng 162px (>=60px) nên đã bổ sung đủ 13 điểm mốc. | Đã sửa |
| `D02.png` | Bàn tay tài xế | `ok` | Xác định đúng tay trái của người lái (side=left) dù ảnh bị xoay 90 độ; không bị nhầm theo hướng màn hình. | Đã chuẩn |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Quên không vẽ skeleton `face13` cho ảnh DMS khi khuôn mặt có độ rộng $\ge 60\text{ px}$, và dễ nhầm lẫn quy ước trái/phải (`side`) của bàn tay theo góc nhìn trên ảnh thay vì theo cơ thể người lái.

Vì sao mình mắc: Do ban đầu tập trung vẽ bounding box nhanh cho kịp tiến độ và chưa quen với góc chụp xoay 90° của camera DMS trong tập dữ liệu Drive&Act.

Lần sau tránh bằng cách: Luôn kiểm tra kích thước chiều rộng của box `face` trước (nếu $\ge 60\text{ px}$ thì bắt buộc tạo skeleton ngay); tưởng tượng bản thân đang ngồi trực tiếp vào vị trí ghế lái để xác định chính xác tay trái / tay phải của tài xế.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó:
- Tại ảnh `S02_rgb.png`, mình đã gán một box `person` cho hình nộm trẻ em ở ghế giữa, trong khi bạn cặp của mình (`peer`) không gán `person`. Khi đối chiếu lại mục 3 và mục 4.8 của Guideline (*"Bộ ảnh không có trẻ em ngồi, thấy hình giống trẻ em thì không gán person"*), mình nhận ra bạn ấy đã đọc kỹ quy tắc đặc thù của bộ dữ liệu dựng SVIRO hơn. Mình đã học được rằng trong gán nhãn AI, không được suy đoán cảm tính theo hình ảnh thấy được mà phải tuân thủ nghiêm ngặt định nghĩa lớp và giới hạn dữ liệu của dự án.

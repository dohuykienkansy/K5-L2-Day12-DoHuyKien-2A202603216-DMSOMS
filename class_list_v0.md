# Danh sách lớp v0 — Đỗ Huy Kiên · G08

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `eye_state` | open / closed / unknown | Phát hiện buồn ngủ (mắt nhắm kéo dài microsleep) để cảnh báo tài xế | Có, trừ khi bị đốm lóa phản xạ đèn LED |
| 2 | `gaze_zone` | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Đánh giá sự tập trung của tài xế vào luồng giao thông | Có, qua hướng mắt và góc xoay đầu |
| 3 | `glasses` | none / clear / sun / unknown | Điều chỉnh thuật toán nhận diện mắt và tròng kính phù hợp | Có, nhận diện được gọng và viền kính |
| 4 | `hand_on_wheel` | yes / no / unknown | Cảnh báo buông tay khỏi vô lăng khi xe yêu cầu tài xế tiếp quản lái (TOR) | Có rõ, nhờ hình thái bàn tay trên vô lăng |
| 5 | `phone_state` | held / mounted / lap | Phát hiện vi phạm sử dụng điện thoại khi đang điều khiển phương tiện | Có, thấy được khối chữ nhật và viền máy |
| 6 | `face_pose_yaw_pitch` | góc yaw, pitch | Cảnh báo mất tập trung khi tài xế quay mặt nói chuyện hoặc cúi đầu quá lâu | Có rất tốt trên ảnh NIR |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `seat_occupancy` | person / empty / object | Bật/tắt cảnh báo thắt dây an toàn cho từng vị trí ghế sau | Có, qua hình khối cơ thể người |
| 2 | `child_seat_presence` | child_seat / infant_seat | Nhắc nhở chống bỏ quên trẻ em trong xe (CPD) và điều chỉnh lực túi khí | Có, thấy được qua hình dạng đặc trưng của ghế |
| 3 | `seatbelt_status` | worn_correct / worn_incorrect / not_worn / unknown | Cảnh báo an toàn hành khách hàng ghế sau | Khá khó trên IR nếu trang phục màu tối |
| 4 | `leftover_object` | bag / box / cup / other | Nhắc nhở hành khách không để quên hành lý, balo, đồ đạc khi rời xe | Có hình dạng nhưng mất dữ liệu màu sắc |
| 5 | `infant_seat_facing` | front / rear | Tự động vô hiệu hóa túi khí phía trước nếu nôi em bé quay về phía sau | Có, thấy rõ chiều xoay của nôi |
| 6 | `passenger_posture` | normal / lying_down / abnormal | Đưa ra cảnh báo nguy hiểm khi hành khách nằm ngả hoặc ngồi sai tư thế | Có rất tốt trên IR nhờ hình thái cơ thể |

## 2 câu hỏi leo thang

1. **Câu hỏi:** Khi tài xế đeo kính râm có lớp tráng chống tia hồng ngoại (NIR-blocking coating) khiến toàn bộ tròng kính biến thành hai đốm đen hoàn toàn không thấy mắt, guideline nên quy định `glasses=sun` hay `glasses=unknown`?
   * **Khung ví dụ:** `D02.png` / `D03.png`
   * **Bạn tạm gán thế nào và vì sao:** Tạm gán `glasses=sun` vì thấy gọng kính dày đặc trưng kính râm và vùng mắt bị chặn sáng hoàn toàn; các điểm mắt gán cờ `outside`.
2. **Câu hỏi:** Một chiếc áo khoác dày đặt phồng lên trên ghế sau có hình thù nhấp nhô giống như một người đang cúi đầu, trong ảnh IR đơn sắc không phân biệt được nhiệt độ hay màu da người, xử lý thế nào để tránh False Positive cho hệ thống túi khí?
   * **Khung ví dụ:** `S05_ir.png`
   * **Bạn tạm gán thế nào và vì sao:** Tạm gán `object` với `type=other` vì không thấy cấu trúc đầu/khuôn mặt rõ ràng, đồng thời đối chiếu với ảnh RGB cùng cảnh nếu có.

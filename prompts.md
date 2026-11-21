# Khai báo dùng AI — Đỗ Huy Kiên

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity AI | Cách gom cùng lúc 22 ảnh từ 2 thư mục oms và driver lên CVAT | Tạo thư mục trung gian upload_cvat để tải lên đồng thời cả 22 ảnh | Kiểm tra lại số lượng hiển thị trên CVAT đủ 22 files |
| 2 | Antigravity AI | Quy ước giải phẫu mắt và tay trên ảnh Drive&Act xoay 90° | Xác định chuẩn mắt trái có tọa độ Y lớn hơn, tay phải ở nửa trên màn hình | Kiểm tra lại bằng script cabin_check.py và hình ảnh giải phẫu |
| 3 | Antigravity AI | Cách phân biệt occupied=yes/no/unknown cho child_seat ở S02 | Chọn đúng occupied=yes cho ghế trẻ em có bé ngồi | Kiểm tra đối chiếu với hướng dẫn của Coach và schema bài lab |
| 4 | Antigravity AI | Cách sửa các cảnh báo WARN về light và cờ occluded mắt | Sửa light=unknown trên SVIRO và đồng bộ cờ occluded trên D06 | Chạy script cabin_check.py đạt 0 lỗi, 0 cảnh báo |

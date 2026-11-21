# TEAM — Ngày 12

Mã bộ ảnh: **G08** · Hình thức: **cá nhân**

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Đỗ Huy Kiên | 2A202603216 | có (kèm 4 ảnh extra S09–S10) | Nguyễn Đức Cường (MSSV: 2A202603040 - G07) | 130 dòng (phân tích toàn bộ & sâu các ca tiêu biểu) |

### 1. Bối cảnh ghép cặp & Phân loại bất đồng
- **Phần OMS (S01–S08):** Bạn Nguyễn Đức Cường (MSSV: 2A202603040) được giao bộ ảnh **G07** (SVIRO set 7), trong khi mình được giao bộ ảnh **G08** (SVIRO BMW X5 set 8). Vì hai bộ ảnh SVIRO này có các kịch bản cabin hoàn toàn khác nhau (ví dụ: ở S07, bài của mình có 2 người lớn `person` + `face`, còn bạn Cường có `child_seat` + `object`), nên khi chạy script diff tự động, hầu hết các nhãn OMS đều có IoU = 0. Trong `disagreement_log.csv`, mình đã ghi chú rõ nguyên nhân và giữ nguyên nhãn chuẩn của bộ G08.
- **Phần DMS (D01–D06):** Cả hai bạn cùng sử dụng chung bộ ảnh Drive&Act NIR thực tế, do đó việc đối chiếu và giải quyết bất đồng guideline là hoàn toàn đồng nhất và hợp lệ.

### 2. Các ca trao đổi đối chiếu theo guideline tiêu biểu:
- `D02.png`: Bạn Cường vẽ box `face` và 13 điểm skeleton dù tài xế đã quay ngoắt mặt ra sau xe. Sau khi cùng mở GUIDE §4.5 đọc quy định *"không thấy cả mắt lẫn mũi thì không vẽ face"*, bạn Cường đã đồng ý phương án của mình là không vẽ face.
- `D06.png`: Bạn Cường gán `seatbelt = not_worn` do nhìn ảnh NIR tối, nhưng khi zoom kỹ thấy dải dây an toàn màu sẫm vắt chéo qua ngực tài xế, hai bạn đã thống nhất là `worn_correct`.
- `D01.png` & `D06.png`: Bật cờ `occluded=1` ở mắt phải do bị đốm LED hồng ngoại chiếu lóa tròng kính theo GUIDE §4.6.
- `S02_rgb.png`: Bạn Cường gán hình đứa trẻ ngồi trong ghế là `person`. Mình giải thích theo GUIDE §3 là không gán trẻ em thành `person` mà gán `child_seat` (`occupied = yes` / `unknown`), bạn đã đồng ý.

## Cá nhân

### DoHuyKien-2A202603216
- Phần mình làm: Hoàn thành đầy đủ 22 ảnh cốt lõi (S01–S08, D01–D06) và 4 ảnh mở rộng extra (S09–S10). Tự kiểm tra bằng script `cabin_check.py` đạt 0 lỗi, 0 cảnh báo ở cả task chính lẫn task extra. Thực hiện diff và phân tích toàn bộ 130 dòng bất đồng với bạn Nguyễn Đức Cường (MSSV: 2A202603040).
- Điều mình học được hôm nay: Hiểu sâu sắc về hệ thống giám sát cabin (OMS và DMS), sự khác biệt giữa IR mô phỏng và IR thật (hiện tượng xuyên thấu kính râm và đốm lóa LED), cũng như tầm quan trọng của việc gọi vị trí theo xe và giải phẫu người lái.

# Tự đánh giá — Đỗ Huy Kiên · G08

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S01_rgb` | `person` | `seat_flip` | Lúc đầu quen mắt nhìn nhầm trái ảnh là `rear_left`, đã sửa lại thành `rear_right` theo xe | Đã sửa |
| `S04_ir` | `object` | `ok` | Hộp bìa carton `type=box` ở `rear_right` rõ ràng hình khối vuông | Đã sửa |
| `D01` | `face` | `flag` | Mắt phải bị đốm LED lóa, chọn `eye_right=unknown` và bật cờ `occluded=1` ở 4 điểm mắt phải | Đã sửa |
| `D04` | `person` | `guess` | Không đoán mò thắt dây, nhìn kỹ thấy khóa kéo áo khoác chạy thẳng tưng nên gán `seatbelt=not_worn` | Đã sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

* **Lỗi:** Quên đảo chiều ghế sau (gán theo ảnh thay vì theo xe) và nhầm lẫn cờ `occluded` giữa mắt trái và mắt phải trên ảnh Drive&Act xoay 90°.
* **Vì sao mình mắc:** Do thói quen thị giác thông thường mà quên mất camera OMS nhìn ngược về phía sau xe (nên trái ảnh là phải xe), và ảnh DMS bị xoay 90° khiến mắt trái nằm ở phía dưới màn hình (tọa độ Y lớn hơn mắt phải).
* **Lần sau tránh bằng cách:** Luôn nhẩm câu thần chú *"trái ảnh là phải xe"* trước khi dán nhãn OMS, và nghiêng đầu 90° chỉ tay vào mắt trái của chính mình để định vị chuẩn xác trên ảnh DMS.

## 3. Ghi chú về disagreement_log & Quá trình đối chiếu chéo

1. **Phân biệt hai bộ dữ liệu khi ghép cặp chéo:**
   - Mình làm bộ **G08** (SVIRO BMW X5 - `set8`), còn bạn Nguyễn Đức Cường (MSSV: `2A202603040`) làm bộ **G07** (SVIRO `set7`). Do đó, ở phần OMS (S01–S08), kịch bản vật thể hoàn toàn khác nhau (ví dụ: S07 của mình là 2 người lớn `person` + `face`, còn bạn Cường là `child_seat` + `object`), dẫn đến IoU = 0 khi diff tự động. Mình đã xác định rõ lý do này trong log và giữ nguyên nhãn theo đúng kịch bản chuẩn G08.
   - Ở phần DMS (D01–D06), cả 2 bạn cùng dùng ảnh Drive&Act NIR thực tế nên dữ liệu hoàn toàn tương đương để so sánh kỹ thuật.

2. **Dòng bất đồng tiêu biểu nhất ở ảnh `D02.png`:**
   - Bạn Cường (MSSV: `2A202603040`) vẫn vẽ box `face` và 13 điểm skeleton `face13` dù tài xế đã quay ngoắt đầu ra phía sau xe.
   - Bài của mình đúng theo **GUIDE §4.5**: *"không thấy mặt (quay đi, bị che gần hết, không thấy cả mắt lẫn mũi) thì không vẽ box face"*.
   - Sau khi đối chiếu guideline, bạn Cường đã đồng ý phương án không vẽ face ở góc này.

3. **Bài học rút ra:**
   - Luôn tuân thủ nguyên tắc "thấy gì gán nấy, không thấy thì không gán/unknown". Không được vẽ theo quán tính hay phỏng đoán khi đối tượng bị khuất hoàn toàn.
   - Khi làm việc theo nhóm hoặc review chéo, luôn kiểm tra mã dataset (`Gxx`) và manifest trước khi diff để phân biệt chính xác giữa khác biệt do bộ ảnh và khác biệt do chất lượng dán nhãn.

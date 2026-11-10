# Báo cáo cá nhân — Ngày 2 Object Detection

## 1. Thông tin học viên

- Họ tên: Lam Trung Hieu
- MSSV: 03048
- Email: onemarketkn@gmail.com
- Lớp: K5 L2A
- Link repo bài làm: https://github.com/lamtrunghieu031002/K5-L2A-Day02-LamTrungHieu-03048
- Link Colab đã chạy: _(điền sau khi chạy xong Colab)_

## 2. Schema và mini guideline

Xem định nghĩa đầy đủ tại [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md).

**Tóm tắt ba ca mơ hồ đã quyết định:**

1. **drive_026 — Van vs Bus**: Xe thân hộp dài ở góc phải ảnh. Quyết định `bus` vì quan sát thấy nhiều cửa sổ xếp đều liên tục theo hàng ngang — đặc điểm phân biệt với van.
2. **drive_019 — Van bị che bởi bus**: Chỉ thấy nửa thân sau của van đứng sau xe buýt. Quyết định `van` vì hình dạng thân hộp nhận biết được; box chỉ bao phần nhìn thấy.
3. **drive_024 — Xe nhỏ ở xa, car vs van**: Xe hàng xa gần đỉnh ảnh, kích thước nhỏ. Quyết định `van` vì mái phẳng và thân hộp rõ, khác với đường cong khoang hành khách của car.

**Phần cần giảng viên làm rõ:** Ranh giới giữa xe bán tải nhỏ (pickup truck nhỏ) và `car`; bài này không gặp ca nào rõ ràng nhưng vẫn ghi nhận.

## 3. Annotation và self-QC

- Số file nhãn train: **50 file** trong `dataset/labels/train/`
- Kết quả checker: **ĐẠT 50/50** — không có lỗi cấu trúc, class ID, hay box vượt biên
- Danh sách 10 ảnh đã rà bằng mắt: drive_001, drive_005, drive_009, drive_014, drive_019, drive_024, drive_026, drive_033, drive_041, drive_048
- Lỗi phát hiện khi rà và cách sửa: Phát hiện một số box hơi lỏng ở các xe nhỏ hàng xa trong drive_024 và drive_026; đã điều chỉnh lại cạnh box bám sát hơn vào thân xe. Không có lỗi sai class phát hiện khi rà mắt.
- Commit khóa nhãn ban đầu: `bd194d8` — "Add YOLO annotations for 50 train images + annotation evaluation results"

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 653 | — |
| FP | 0 | — |
| FN | 0 | — |
| Precision | 1.000 | — |
| Recall | 1.000 | — |
| F1 | 1.000 | — |
| mean_iou_of_matches | 0.8425 | — |
| passed | true | — |

Xem kết quả đầy đủ tại [`outputs/annotation_evaluation.json`](../../outputs/annotation_evaluation.json).

**Nhận xét:** Kết quả đạt ngưỡng (F1 >= 0.80 và mean IoU >= 0.70) ngay lần đầu, không cần rework. TP=653 khớp với tổng số box đã gán; FP=0 và FN=0 cho thấy không có box thừa và không bỏ sót xe nào trong gold set. mean_iou_of_matches=0.8425 cho thấy các box bám sát tốt.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: _(điền sau khi chạy Colab)_
- Các tham số thay đổi so với notebook nếu có và lý do: _(điền sau khi chạy Colab)_
- Đường dẫn best checkpoint trong phiên chạy: _(điền sau khi chạy Colab)_

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | _(Colab)_ |
| Recall | _(Colab)_ |
| mAP50 | _(Colab)_ |
| mAP50–95 | _(Colab)_ |

_(Điền ảnh eval_predictions/ và yolo26_runs/ sau khi giải nén day2_colab_outputs.zip vào assets/)_

**Trả lời bốn câu hỏi cuối notebook:** _(điền sau khi chạy Colab và quan sát kết quả thực tế)_

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Gán nhãn — xe nhỏ hàng xa | Khó phân biệt `car` và `van` khi kích thước box rất nhỏ | Zoom ảnh để quan sát hình dạng mái và thân | Phân biệt được dựa trên mái phẳng (van) vs cong (car) |
| Gán nhãn — xe bị che | Không chắc nên box đến đâu khi xe bị che >50% | Áp dụng quy tắc: box chỉ bao phần nhìn thấy | Nhất quán trong toàn bộ bộ nhãn |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md):

| Tiêu chí | Trạng thái |
|---|---|
| Hoàn thành và định dạng YOLO (10đ) | Đạt — 50/50 file, checker pass, 5 cột, class 0–3 |
| Đầy đủ vật thể (20đ) | Đạt — TP=653, FN=0 |
| Độ bám sát và hình học box (20đ) | Đạt — mean_iou=0.8425, không có FP |
| Phân lớp nhất quán (15đ) | Đạt — precision=1.0, không nhầm class |
| Mini guideline và quyết định mơ hồ (10đ) | Đạt — 4 lớp định nghĩa, 3 ca có lý do |
| Gold-set annotation QC (15đ) | Đạt — F1=1.0, mean IoU=0.8425 >= 0.70 |
| Pipeline YOLO và phân tích (10đ) | Chờ chạy Colab |

## 8. Công cụ AI và tài liệu tham khảo

- **Công cụ annotation:** CVAT — dùng để vẽ bounding box và xuất nhãn YOLO detection format cho 50 ảnh train.
- **Claude Code (AI assistant):** hỗ trợ điền GUIDELINE_MINI.md và báo cáo sau khi cung cấp thông tin cá nhân và kết quả thực tế; không dùng để tạo nhãn.
- **Nguồn tài liệu:** tài liệu trong repository (`GUIDE.md`, `RULES.md`, `RUBRIC.md`); không dùng nguồn ngoài để tìm nhãn hoặc gold labels.
- Không gán nhãn từ nguồn bên ngoài; không dùng gold train làm nhãn của mình.

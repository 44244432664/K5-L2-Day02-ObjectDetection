# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Nguyễn Hải Đăng
- MSSV: 2A202603190
- Email: haidang453@gmail.com
- Lớp: 2a
- Link repo bài làm: https://github.com/44244432664/K5-L2-Day02-ObjectDetection.git
- Link Colab đã chạy: https://colab.research.google.com/drive/1mZlScUyW9FMR9QHKMeXC6dhxkY3bguIs?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

Schema giữ nguyên bốn lớp: `0 = car`, `1 = truck`, `2 = bus`, `3 = van`. Box bám sát phần xe nhìn thấy, không lấy bóng đổ/nền và không suy đoán phần bị che hoặc nằm ngoài ảnh.

Giảng viên đã làm rõ hai phần **Vật thể bị cắt bởi rìa ảnh** và **Vật thể rất nhỏ/mơ hồ**. Theo mini guideline hiện có: với xe bị cắt khung, chỉ bao phần xe nằm trong ảnh và đặt cạnh box sát rìa tương ứng; với xe rất nhỏ/mơ hồ, phóng to kiểm tra, chỉ gán lớp khi đủ đặc điểm nhận diện, ghi lại trường hợp chưa rõ để hỏi giảng viên.

Ba ca mơ hồ đối chiếu từ ảnh và nhãn hiện có:

1. **Xe bị cắt bởi rìa ảnh — [drive_003.jpg](../../dataset/images/train/drive_003.jpg):** xe buýt ở mép phải được [nhãn hiện tại](../../dataset/labels/train/drive_003.txt) ghi `bus` tại tâm normalized xấp xỉ `(0.971, 0.232)`; cạnh phải box đạt xấp xỉ `1.0`. Áp dụng quy tắc chỉ bao phần xe trong khung, không ước lượng phần nằm ngoài ảnh.
2. **Xe rất nhỏ — [drive_002.jpg](../../dataset/images/train/drive_002.jpg):** vật thể ở xa phía trên ảnh được [nhãn hiện tại](../../dataset/labels/train/drive_002.txt) ghi `car` tại tâm `(0.619, 0.115)`, box rộng/cao normalized xấp xỉ `(0.0123, 0.0174)`. Quy tắc áp dụng là phóng to để kiểm tra đủ đặc điểm phân lớp; không suy đoán lớp chỉ từ kích thước hoặc bối cảnh. Việc nhãn hiện tại ghi `car` không tự chứng minh vật thể đã được nhận diện đúng.
3. **Xe bị che một phần — [drive_001.jpg](../../dataset/images/train/drive_001.jpg):** xe trắng ở làn bên phải bị cột che một phần được [nhãn hiện tại](../../dataset/labels/train/drive_001.txt) ghi `car` tại tâm xấp xỉ `(0.793, 0.555)`. Quy tắc áp dụng là một box cho cùng một xe, bao các phần nhìn thấy và không suy đoán phần bị che.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: Đã chạy lại bằng `.venv`; terminal trả về “ĐẠT cấu trúc: 50/50 file nhãn hợp lệ”
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: [drive_001.jpg](../../dataset/images/train/drive_001.jpg) ([nhãn](../../dataset/labels/train/drive_001.txt)), [drive_002.jpg](../../dataset/images/train/drive_002.jpg) ([nhãn](../../dataset/labels/train/drive_002.txt)), [drive_003.jpg](../../dataset/images/train/drive_003.jpg) ([nhãn](../../dataset/labels/train/drive_003.txt)), [drive_004.jpg](../../dataset/images/train/drive_004.jpg) ([nhãn](../../dataset/labels/train/drive_004.txt)), [drive_005.jpg](../../dataset/images/train/drive_005.jpg) ([nhãn](../../dataset/labels/train/drive_005.txt)), [drive_006.jpg](../../dataset/images/train/drive_006.jpg) ([nhãn](../../dataset/labels/train/drive_006.txt)), [drive_007.jpg](../../dataset/images/train/drive_007.jpg) ([nhãn](../../dataset/labels/train/drive_007.txt)), [drive_008.jpg](../../dataset/images/train/drive_008.jpg) ([nhãn](../../dataset/labels/train/drive_008.txt)), [drive_009.jpg](../../dataset/images/train/drive_009.jpg) ([nhãn](../../dataset/labels/train/drive_009.txt)), [drive_010.jpg](../../dataset/images/train/drive_010.jpg) ([nhãn](../../dataset/labels/train/drive_010.txt)).
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
- Commit khóa nhãn ban đầu: `dc5968a7393d3fd9fa23a7aaa2407dec4a6c4eba` (`add images`, 09/11/2026 19:41:22 UTC+7), là commit đầu tiên lưu đủ 50 file nhãn train theo lịch sử Git.

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 441 | |
| FP | 691 | |
| FN | 212 | |
| Precision | 0.3896 | |
| Recall | 0.6753 | |
| F1 | 0.4941 | |
| mean_iou_of_matches | 0.8529 | |
| passed | `false` | |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

**Rework: không thực hiện do không đủ thời gian.** Giữ nguyên kết quả đánh giá hiện có; cột **Sau sửa nếu có** để trống vì không có vòng sửa và đánh giá lại sau sửa.

Kết quả: [annotation_evaluation.json](../../outputs/annotation_evaluation.json). Lệnh đã chạy lại từ thư mục gốc bằng Python trong `.venv`:

```powershell
.\.venv\Scripts\python.exe tools/evaluate_annotations.py --student-labels dataset/labels/train --gold-labels gold_train_labels
```

**Chưa đạt**: F1 = 0.4941 < 0.80; mean_iou_of_matches = 0.8529 ≥ 0.70. Script dùng ngưỡng ghép IoU = 0.50, cùng lớp và một-một; trả về mã thoát `1` vì chưa đạt cổng QC.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Google Colab, GPU NVIDIA T4; Ultralytics v0.0.8, Torch 2.14.1+cu130
- Các tham số thay đổi so với notebook nếu có và lý do: Không
- Đường dẫn best checkpoint trong phiên chạy: `K5-L2-Day02-ObjectDetection\report\individual\assets\yolo26_runs\vehicle_annotation\weights\best.pt`.

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.4105 |
| Recall | 0.2303 |
| mAP50 | 0.2723 |
| mAP50–95 | 0.2017 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Các chỉ số YOLO lấy từ [model_eval_metrics.json](assets/model_eval_metrics.json) đã có; lệnh evaluate vừa chạy chỉ đánh giá annotation, không tính lại metric mô hình. Đã có [10 ảnh dự đoán eval](assets/eval_predictions/visuals/) và [log/ảnh chỉ số YOLO](assets/yolo26_runs/). Ví dụ trong [drive_051.jpg](assets/eval_predictions/visuals/drive_051.jpg), xe đỏ lớn phía dưới bên trái được dự đoán `van 0.99`, trong khi [nhãn eval](../../dataset/labels/eval/drive_051.txt) ghi `car` tại tâm normalized xấp xỉ `(0.348, 0.836)`.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?

   Theo [confusion matrix eval](assets/yolo26_runs/vehicle_eval/confusion_matrix.png), `bus` và `van` đều có TP = 0, lần lượt trên 2 và 12 vật thể thật, nên recall tính từ ma trận là 0. Trong [drive_052.jpg](assets/eval_predictions/visuals/drive_052.jpg), vật thể lớn giữa ảnh, lệch trái, được dự đoán `bus 0.51`; [nhãn eval](../../dataset/labels/eval/drive_052.txt) ghi `van` tại tâm `(0.427, 0.534)`. JSON chỉ lưu recall tổng hợp, chưa có bảng recall từng lớp tại ngưỡng tính metric.

2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?

   Cần kiểm vị trí và độ bám sát các cạnh box, phần nền lấy dư, phần xe bị cắt hoặc bị che. Box có thể đạt IoU 0.50 nhưng không đạt ngưỡng cao hơn. Kết quả hiện tại có mAP50 = 0.2723, chưa phải trường hợp mAP50 cao.

3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?

   Ma trận ghi nhận 11 vật thể thật `van` được dự đoán `bus` và 4 `truck` được dự đoán `car`; các ảnh trên minh họa thêm bất đồng class. Cần đối chiếu ranh giới lớp trong guideline với ảnh và nhãn train; chưa đủ căn cứ quy nguyên nhân cho guideline cá nhân hoặc kết luận nhãn eval sai.

4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?

   [data.yaml](../../data.yaml) tách `train: images/train` và `val: images/eval`. Theo notebook, eval dùng để validation khi train, chọn `best.pt` và tính metric cuối. Đưa eval vào train làm mất sự tách biệt giữa dữ liệu huấn luyện và đánh giá. Vì đã tham gia chọn checkpoint, eval không phải test set độc lập.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| xác định label `van` vs `car` | khó phân biệt giữa `van` và `car` do có vẻ ngoài gần tương tự nhau | sử dụng `GUIDELINE_MINI.md` để xác định vẻ ngoài của phương tiện | Gold QC hiện tại chưa đạt: Precision = 0.3896, F1 = 0.4941 |
| xác định ảnh phương tiện trong các ảnh có nhiều phương tiện chồng lên nhau | xác định có nên đóng khung (box) vật thể không | đọc lại `GUIDELINE` và tham khảo ý kiến giảng viên | Gold QC tổng hợp ghi nhận FP = 691, FN = 212, mean_iou_of_matches = 0.8529 và passed = false. Chưa xác định các sai khác thuộc vật thể chồng lấp |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

Đã có 50 file nhãn qua checker, JSON gold QC, metric YOLO, 10 ảnh dự đoán eval, danh sách 10 ảnh đầu đã tự tái kiểm tra, commit nhãn ban đầu và thông tin runtime Google Colab/GPU T4. Mục 2 đã đối chiếu ba ca mơ hồ từ ảnh và nhãn hiện có; bảng ba ca mơ hồ trong `GUIDELINE_MINI.md` vẫn cần cập nhật tương ứng. Gold QC chưa đạt F1; mean IoU chỉ xác nhận độ khớp của các cặp đã ghép. Không rework do không đủ thời gian.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.

Đã tự kiểm tra lại 10 ảnh đầu (`drive_001`–`drive_010`) và kết quả từ script `tools/evaluate_annotations.py`. Sử dụng ChatGPT/Codex để tổng hợp thông tin, đối chiếu tài liệu và hỗ trợ diễn đạt báo cáo. Tài liệu tham khảo trong lần tổng hợp này gồm `GUIDELINE_MINI.md`, `RUBRIC.md`, `SUBMISSION.md`, notebook, scripts và artifacts trong repo.
